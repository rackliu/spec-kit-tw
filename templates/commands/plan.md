---
description: 執行實施規劃工作流, 使用計劃模板生成設計製品.
handoffs:
  - label: 建立任務
    agent: speckit.tasks
    prompt: 將計劃分解為任務
    send: true
  - label: 建立檢查清單
    agent: speckit.checklist
    prompt: 為需求建立品質檢查清單
    send: true
scripts:
  sh: scripts/bash/setup-plan.sh --json
  ps: scripts/powershell/setup-plan.ps1 -Json
agent_scripts:
  sh: scripts/bash/update-agent-context.sh __AGENT__
  ps: scripts/powershell/update-agent-context.ps1 -AgentType __AGENT__
---

## 使用者輸入

```text
$ARGUMENTS
```

在繼續之前, 你**必須**考慮使用者輸入(如果不為空).

## 大綱

1. **設定**: 從倉庫根目錄執行 `{SCRIPT}` 並解析 JSON 獲取 FEATURE_SPEC、IMPL_PLAN、SPECS_DIR、BRANCH. 對於引數中的單引號如 "I'm Groot", 使用轉義語法: 例如 'I'\''m Groot'(或儘可能使用雙引號: "I'm Groot").

2. **載入上下文**: 讀取 FEATURE_SPEC 和 `/memory/constitution.md`. 載入 IMPL_PLAN 模板(已複製).

3. **執行計劃工作流**: 按照 IMPL_PLAN 模板中的結構: 
   - 填充技術上下文(將未知項標記為 NEEDS CLARIFICATION)
   - 從章程文件填充章程檢查部分
   - 評估關卡(如果違規無正當理由則報錯)
   - 階段 0: 生成 research.md(解決所有 NEEDS CLARIFICATION)
   - 階段 1: 生成 data-model.md、contracts/、quickstart.md
   - 階段 1: 透過執行代理指令碼更新代理上下文
   - 設計後重新評估章程檢查

4. **停止並報告**: 命令在階段 2 規劃後結束. 報告分支、IMPL_PLAN 路徑和生成的製品.

## 階段

### 階段 0: 大綱與研究

1. **從上述技術上下文中提取未知項**: 
   - 每個 NEEDS CLARIFICATION → 研究任務
   - 每個依賴項 → 最佳實踐任務
   - 每個整合 → 模式任務

2. **生成和分發研究代理**: 
   ```
   For each unknown in Technical Context:
     Task: "Research {unknown} for {feature context}"
   For each technology choice:
     Task: "Find best practices for {tech} in {domain}"
   ```

3. **在 `research.md` 中整合發現**, 使用格式: 
   - Decision: [選擇了什麼]
   - Rationale: [為什麼選擇]
   - Alternatives considered: [還評估了什麼]

**輸出**: research.md, 所有 NEEDS CLARIFICATION 已解決

### 階段 1: 設計與合同

**前提條件**: `research.md` 完成

1. **從功能規格中提取實體** → `data-model.md`: 
   - 實體名稱、欄位、關係
   - 來自需求的驗證規則
   - 狀態轉換(如適用)

2. **從功能需求生成 API 合同**: 
   - 每個使用者操作 → 端點
   - 使用標準 REST/GraphQL 模式
   - 將 OpenAPI/GraphQL 模式輸出到 `/contracts/`

3. **代理上下文更新**: 
   - 執行 `{AGENT_SCRIPT}`
   - 這些指令碼檢測正在使用哪個 AI 代理
   - 更新相應的代理特定上下文檔案
   - 僅添加當前計劃中的新技術
   - 保留標記之間的手動新增內容

**輸出**: data-model.md、/contracts/*、quickstart.md、代理特定檔案

## 關鍵規則

- 使用絕對路徑
- 關卡失敗或未解決的澄清事項時報錯
