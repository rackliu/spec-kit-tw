---
name: translation-workflow
description: "翻譯工作流管理 - 提供完整的使用指南和最佳實踐"
---

使用者輸入: 
$ARGUMENTS

目標: 為翻譯專案提供完整的工作流指南, 確保團隊能夠高效使用自動化翻譯系統.

## 工作流概覽

### 核心命令體系
```
translation-auto      # 全自動翻譯(一鍵式)
translation-sync      # 同步原版更新
translation-detect    # 檢測翻譯需求
translation-execute   # 執行翻譯任務
translation-qa        # 品質保證檢查
translation-fix       # 修復翻譯問題
translation-review    # 人工稽核(已存在)
```

### 推薦工作流程

#### 1. 首次設定翻譯專案
```bash
/translation-detect    # 檢測需要翻譯的檔案
/translation-auto      # 執行完整翻譯流程
/translation-qa        # 品質檢查
/translation-fix       # 修復發現的問題
```

#### 2. 原版更新後的同步
```bash
/translation-sync      # 同步原版更新
/translation-qa        # 驗證同步品質
/translation-fix       # 修復同步問題
```

#### 3. 日常翻譯維護
```bash
/translation-detect    # 檢測新增翻譯需求
/translation-execute   # 執行翻譯
/translation-qa        # 品質檢查
```

#### 4. 釋出前品質檢查
```bash
/translation-qa        # 全面品質檢查
/translation-fix       # 修復關鍵問題
/translation-review    # 最終人工稽核
```

## 最佳實踐指南

### 自動化策略
1. **最大化自動化**: 優先使用 `translation-auto` 處理常規翻譯任務
2. **增量更新**: 使用 `translation-sync` 進行增量更新, 避免重複工作
3. **品質優先**: 每次翻譯後都要執行 `translation-qa` 進行品質檢查
4. **持續改進**: 定期使用 `translation-fix` 最佳化翻譯品質

### 品質保證策略
1. **多層檢查**: 自動化檢查 + 人工稽核的雙重保障
2. **重點關注**: CLI相關檔案和核心模板需要更嚴格檢查
3. **一致性維護**: 定期檢查術語使用和翻譯風格一致性
4. **使用者反饋**: 建立使用者反饋機制, 持續改進翻譯品質

### 風險控制策略
1. **分支操作**: 所有翻譯操作都在分支進行, 確保主分支穩定
2. **漸進式釋出**: 分階段釋出翻譯更新, 降低風險
3. **回滾準備**: 保持回滾能力, 快速響應問題

## 常見場景處理

### 場景1: 原版大版本更新
```bash
# 推薦流程
/translation-sync      # 智慧同步更新
/translation-qa        # 全面品質檢查
/translation-fix       # 修復問題
/translation-review    # 人工稽核關鍵檔案
```

### 場景2: 發現翻譯錯誤
```bash
# 針對性修復
/translation-detect    # 定位問題檔案
/translation-fix       # 智慧修復
/translation-qa        # 驗證修復效果
```

### 場景3: 新增功能翻譯
```bash
# 快速響應
/translation-detect    # 識別新增內容
/translation-execute   # 快速翻譯
/translation-qa        # 品質驗證
```

### 場景4: 釋出前檢查
```bash
# 全面檢查
/translation-qa        # 完整品質檢查
/translation-fix       # 修復所有問題
/translation-review    # 最終稽核
```

## 效能最佳化建議

### 並行處理
- 利用Task工具並行處理多個檔案
- 合理分配翻譯任務, 提高效率
- 監控系統資源使用情況

### 快取策略
- 建立翻譯記憶庫, 避免重複翻譯
- 快取常用術語和表達方式
- 保持翻譯風格一致性

### 增量處理
- 僅處理變更內容, 避免全量重翻
- 智慧識別翻譯需求, 精確處理
- 保持現有翻譯穩定性

## 團隊協作指南

### 角色分工
- **翻譯負責人**: 負責整體翻譯策略和品質把控
- **技術稽核**: 負責CLI功能和技術準確性驗證
- **語言稽核**: 負責翻譯品質和語言表達最佳化
- **使用者測試**: 負責使用者體驗和實際使用驗證

### 協作流程
1. **需求分析**: 使用 `translation-detect` 分析翻譯需求
2. **任務分配**: 基於檢測結果分配翻譯任務
3. **並行執行**: 使用 `translation-execute` 並行處理
4. **品質檢查**: 使用 `translation-qa` 統一品質標準
5. **問題修復**: 使用 `translation-fix` 處理品質問題
6. **最終稽核**: 使用 `translation-review` 人工稽核

### 溝通機制
- 建立翻譯問題反饋渠道
- 定期召開翻譯品質評審會議
- 維護翻譯知識庫和最佳實踐
- 跟蹤翻譯指標和持續改進

## 監控和度量

### 品質指標
- 翻譯完成度
- 術語一致性率
- 使用者反饋評分
- 問題修復率

### 效率指標
- 翻譯速度
- 自動化率
- 人工干預率
- 釋出週期

### 持續改進
- 定期分析翻譯資料
- 最佳化翻譯流程
- 更新翻譯標準
- 改進自動化工具

行為規則: 
- 根據專案具體情況選擇合適的工作流程
- 保持翻譯品質和效率的平衡
- 重視使用者反饋和持續改進
- 建立完善的翻譯知識管理體系
- 確保團隊協作的高效性和一致性
