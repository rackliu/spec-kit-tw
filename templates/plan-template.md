# 實施計劃: [FEATURE]

**分支**: `[###-feature-name]` | **日期**: [DATE] | **規格**: [link]
**輸入**: 來自 `/specs/[###-feature-name]/spec.md` 的功能規格

**注意**: 此模板由 `/speckit.plan` 命令填充. 執行工作流程請參見 `.specify/templates/commands/plan.md`.

## 摘要

[從功能規格中提取: 主要需求 + 研究得出的技術方法]

## 技術背景

<!--
  需要操作: 將此部分內容替換為專案的技術細節.
  此處的結構以諮詢性質呈現, 用於指導迭代過程.
-->

**語言/版本**: [例如: Python 3.11、Swift 5.9、Rust 1.75 或 NEEDS CLARIFICATION]
**主要依賴**: [例如: FastAPI、UIKit、LLVM 或 NEEDS CLARIFICATION]
**儲存**: [如適用, 例如: PostgreSQL、CoreData、檔案 或 N/A]
**測試**: [例如: pytest、XCTest、cargo test 或 NEEDS CLARIFICATION]
**目標平臺**: [例如: Linux 伺服器、iOS 15+、WASM 或 NEEDS CLARIFICATION]
**專案型別**: [單一/網頁/移動 - 決定原始碼結構]
**效能目標**: [領域特定, 例如: 1000 請求/秒、10k 行/秒、60 fps 或 NEEDS CLARIFICATION]
**約束條件**: [領域特定, 例如: <200ms p95、<100MB 記憶體、離線可用 或 NEEDS CLARIFICATION]
**規模/範圍**: [領域特定, 例如: 10k 使用者、1M 行程式碼、50 個螢幕 或 NEEDS CLARIFICATION]

## 章程檢查

*門控: 必須在階段 0 研究前透過. 階段 1 設計後重新檢查. *

[基於章程檔案確定的門控條件]

## 專案結構

### 文件(此功能)

```
specs/[###-feature]/
├── plan.md              # 此檔案 (/speckit.plan 命令輸出)
├── research.md          # 階段 0 輸出 (/speckit.plan 命令)
├── data-model.md        # 階段 1 輸出 (/speckit.plan 命令)
├── quickstart.md        # 階段 1 輸出 (/speckit.plan 命令)
├── contracts/           # 階段 1 輸出 (/speckit.plan 命令)
└── tasks.md             # 階段 2 輸出 (/speckit.tasks 命令 - 非 /speckit.plan 建立)
```

### 原始碼(倉庫根目錄)
<!--
  需要操作: 將下面的佔位符樹結構替換為此功能的具體佈局.
  刪除未使用的選項, 並使用真實路徑(例如: apps/admin、packages/something)擴充套件所選結構.
  交付的計劃不得包含選項標籤.
-->

```
# [如未使用請刪除] 選項 1: 單一專案(預設)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [如未使用請刪除] 選項 2: Web 應用程式(檢測到"前端" + "後端"時)
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [如未使用請刪除] 選項 3: 移動端 + API(檢測到 "iOS/Android" 時)
api/
└── [同上後端結構]

ios/ 或 android/
└── [平臺特定結構: 功能模組、UI 流程、平臺測試]
```

**結構決策**: [記錄所選結構並引用上面捕獲的真實目錄]

## 複雜度跟蹤

*僅在章程檢查有必須證明的違規時填寫*

| 違規 | 為什麼需要 | 拒絕更簡單替代方案的原因 |
|-----------|------------|-------------------------------------|
| [例如: 第 4 個專案] | [當前需求] | [為什麼 3 個專案不夠] |
| [例如: 倉儲模式] | [特定問題] | [為什麼直接資料庫訪問不夠] |
