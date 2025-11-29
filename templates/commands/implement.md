---
description: 透過處理和執行 tasks.md 中定義的所有任務來執行實施計劃
scripts:
  sh: scripts/bash/check-prerequisites.sh --json --require-tasks --include-tasks
  ps: scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks
---

## 使用者輸入

```text
$ARGUMENTS
```

在繼續之前, 你**必須**考慮使用者輸入(如果不為空).

## 概要

1. 從倉庫根目錄執行 `{SCRIPT}` 並解析 FEATURE_DIR 和 AVAILABLE_DOCS 列表. 所有路徑必須是絕對路徑. 對於引數中的單引號如 "I'm Groot", 使用轉義語法: 例如 'I'\''m Groot'(或儘可能使用雙引號: "I'm Groot").

2. **檢查清單狀態**(如果 FEATURE_DIR/checklists/ 存在): 
   - 掃描 checklists/ 目錄中的所有清單檔案
   - 對於每個清單, 統計: 
     * 總專案數: 所有匹配 `- [ ]` 或 `- [X]` 或 `- [x]` 的行
     * 已完成專案數: 匹配 `- [X]` 或 `- [x]` 的行
     * 未完成專案數: 匹配 `- [ ]` 的行
   - 建立狀態表: 
     ```
     | Checklist | Total | Completed | Incomplete | Status |
     |-----------|-------|-----------|------------|--------|
     | ux.md     | 12    | 12        | 0          | ✓ PASS |
     | test.md   | 8     | 5         | 3          | ✗ FAIL |
     | security.md | 6   | 6         | 0          | ✓ PASS |
     ```
   - 計算總體狀態: 
     * **PASS**: 所有清單都有 0 個未完成專案
     * **FAIL**: 一個或多個清單有未完成專案

   - **如果任何清單未完成**: 
     * 顯示包含未完成專案數的表格
     * **停止**並詢問: "Some checklists are incomplete. Do you want to proceed with implementation anyway? (yes/no)"
     * 在繼續之前等待使用者響應
     * 如果使用者說 "no" 或 "wait" 或 "stop", 停止執行
     * 如果使用者說 "yes" 或 "proceed" 或 "continue", 繼續到步驟 3

   - **如果所有清單都已完成**: 
     * 顯示顯示所有清單透過的表格
     * 自動繼續到步驟 3

3. 載入和分析實施上下文: 
   - **必需**: 讀取 tasks.md 獲取完整任務列表和執行計劃
   - **必需**: 讀取 plan.md 獲取技術棧、架構和檔案結構
   - **如果存在**: 讀取 data-model.md 獲取實體和關係
   - **如果存在**: 讀取 contracts/ 獲取 API 規格和測試要求
   - **如果存在**: 讀取 research.md 獲取技術決策和約束
   - **如果存在**: 讀取 quickstart.md 獲取整合場景

4. **專案設定驗證**: 
   - **必需**: 基於實際專案設定建立/驗證忽略檔案: 

   **檢測和建立邏輯**: 
   - 檢查以下命令是否成功以確定是否為 git 倉庫(如果是, 建立/驗證 .gitignore): 

     ```sh
     git rev-parse --git-dir 2>/dev/null
     ```
   - 檢查 Dockerfile* 是否存在或 plan.md 中是否提到 Docker → 建立/驗證 .dockerignore
   - 檢查 .eslintrc* 或 eslint.config.* 是否存在 → 建立/驗證 .eslintignore
   - 檢查 .prettierrc* 是否存在 → 建立/驗證 .prettierignore
   - 檢查 .npmrc 或 package.json 是否存在 → 建立/驗證 .npmignore(如果釋出)
   - 檢查 terraform 檔案(*.tf)是否存在 → 建立/驗證 .terraformignore
   - 檢查是否需要 .helmignore(存在 helm charts)→ 建立/驗證 .helmignore

   **如果忽略檔案存在**: 驗證它包含基本模式, 僅追加缺失的關鍵模式
   **如果忽略檔案缺失**: 為檢測到的技術建立完整模式集

   **按技術的通用模式**(來自 plan.md 技術棧):
   - **Node.js/JavaScript**: `node_modules/`, `dist/`, `build/`, `*.log`, `.env*`
   - **Python**: `__pycache__/`, `*.pyc`, `.venv/`, `venv/`, `dist/`, `*.egg-info/`
   - **Java**: `target/`, `*.class`, `*.jar`, `.gradle/`, `build/`
   - **C#/.NET**: `bin/`, `obj/`, `*.user`, `*.suo`, `packages/`
   - **Go**: `*.exe`, `*.test`, `vendor/`, `*.out`
   - **Ruby**: `.bundle/`, `log/`, `tmp/`, `*.gem`, `vendor/bundle/`
   - **PHP**: `vendor/`, `*.log`, `*.cache`, `*.env`
   - **Rust**: `target/`, `debug/`, `release/`, `*.rs.bk`, `*.rlib`, `*.prof*`, `.idea/`, `*.log`, `.env*`
   - **Kotlin**: `build/`, `out/`, `.gradle/`, `.idea/`, `*.class`, `*.jar`, `*.iml`, `*.log`, `.env*`
   - **C++**: `build/`, `bin/`, `obj/`, `out/`, `*.o`, `*.so`, `*.a`, `*.exe`, `*.dll`, `.idea/`, `*.log`, `.env*`
   - **C**: `build/`, `bin/`, `obj/`, `out/`, `*.o`, `*.a`, `*.so`, `*.exe`, `Makefile`, `config.log`, `.idea/`, `*.log`, `.env*`
   - **Swift**: `.build/`, `DerivedData/`, `*.swiftpm/`, `Packages/`
   - **R**: `.Rproj.user/`, `.Rhistory`, `.RData`, `.Ruserdata`, `*.Rproj`, `packrat/`, `renv/`
   - **通用**: `.DS_Store`, `Thumbs.db`, `*.tmp`, `*.swp`, `.vscode/`, `.idea/`

   **工具特定模式**:
   - **Docker**: `node_modules/`, `.git/`, `Dockerfile*`, `.dockerignore`, `*.log*`, `.env*`, `coverage/`
   - **ESLint**: `node_modules/`, `dist/`, `build/`, `coverage/`, `*.min.js`
   - **Prettier**: `node_modules/`, `dist/`, `build/`, `coverage/`, `package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`
   - **Terraform**: `.terraform/`, `*.tfstate*`, `*.tfvars`, `.terraform.lock.hcl`
   - **Kubernetes/k8s**: `*.secret.yaml`, `secrets/`, `.kube/`, `kubeconfig*`, `*.key`, `*.crt`

5. 解析 tasks.md 結構並提取: 
   - **任務階段**: 設定、測試、核心、整合、完善
   - **任務依賴**: 順序執行與並行執行規則
   - **任務詳情**: ID、描述、檔案路徑、並行標記 [P]
   - **執行流程**: 順序和依賴要求

6. 按照任務計劃執行實施: 
   - **分階段執行**: 在進入下一階段之前完成每個階段
   - **遵循依賴**: 按順序執行順序任務, 並行任務 [P] 可以一起執行
   - **遵循 TDD 方法**: 在相應的實施任務之前執行測試任務
   - **基於檔案的協調**: 影響相同檔案的任務必須順序執行
   - **驗證檢查點**: 在繼續之前驗證每個階段的完成

7. 實施執行規則: 
   - **首先設定**: 初始化專案結構、依賴、配置
   - **程式碼前測試**: 如果需要為合約、實體和整合場景編寫測試
   - **核心開發**: 實施模型、服務、CLI 命令、端點
   - **整合工作**: 資料庫連線、中介軟體、日誌、外部服務
   - **完善和驗證**: 單元測試、效能最佳化、文件

8. 進度跟蹤和錯誤處理: 
   - 在每個完成的任務後報告進度
   - 如果任何非並行任務失敗, 停止執行
   - 對於並行任務 [P], 繼續成功的任務, 報告失敗的任務
   - 提供帶有除錯上下文的清晰錯誤訊息
   - 如果實施無法繼續, 建議下一步操作
   - **重要** 對於已完成的任務, 確保在任務檔案中將任務標記為 [X].

9. 完成驗證: 
   - 驗證所有必需任務已完成
   - 檢查實施的功能是否與原始規格匹配
   - 驗證測試透過且覆蓋率滿足要求
   - 確認實施遵循技術計劃
   - 報告最終狀態並附上已完成工作的摘要

注意: 此命令假設 tasks.md 中存在完整的任務分解. 如果任務不完整或缺失, 建議首先執行 `/tasks` 重新生成任務列表.
