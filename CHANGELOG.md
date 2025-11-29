# 變更日誌

本專案的重要變更將記錄在此檔案中.

格式基於[Keep a Changelog](https://keepachangelog.com/zh-TW/1.0.0/),
並且本專案遵循[語義化版本](https://semver.org/lang/zh-TW/).

## [0.0.86] - 2025-11-29

### 同步原版
- 同步原版 [v0.0.86](https://github.com/github/spec-kit/releases/tag/v0.0.86)
- 對應原版範圍: v0.0.78 → v0.0.86

### 🚀 新增功能

#### IBM Bob IDE 支援
- **CLI 整合**: 新增 IBM Bob 配置到 `AGENT_CONFIG`
- **幫助文件**: 更新 `--ai` 引數幫助資訊，包含 IBM Bob 選項
- **代理文件**: 在 `AGENTS.md` 中新增 IBM Bob 條目
- **術語表**: 在 `TERMINOLOGY.md` 中新增 IBM Bob 和 SHAI 術語

#### 檔案同步
- **src/specify_cli/__init__.py**: 同步 IBM Bob 配置和 CLI 幫助資訊
- **AGENTS.md**: 完整翻譯並新增 IBM Bob 支援
- **TERMINOLOGY.md**: 新增 IBM Bob 和 SHAI 術語條目
- **pyproject.toml**: 版本號更新至 v0.0.86
- **README.md**: 驗證已包含最新 AI 助手列表

### 🔧 技術更新
- **構建指令碼**: 同步原版釋出和上下文更新指令碼
- **版本管理**: 遵循語義化版本規格

### 📋 品質保證
- **翻譯標準**: 遵循 TRANSLATION_STANDARDS.md 規格
- **術語一致性**: 確保所有新術語符合 TERMINOLOGY.md
- **功能驗證**: 驗證 IBM Bob 在 CLI 中正常工作

---

*本次同步主要完成 IBM Bob IDE 的支援整合，確保中文版與原版 v0.0.86 保持功能對等。*

### 同步原版
- 同步原版 [v0.0.85](https://github.com/github/spec-kit/releases/tag/v0.0.85)
- 對應原版範圍: v0.0.78 → v0.0.85
- 主要同步提交: `e77d99a Support for version command` 等

### 🚀 新增功能
- **版本命令支援**: 新增 `specify-tw version` 命令
  - 顯示CLI版本和系統資訊
  - 獲取最新模板版本資訊
  - 顯示Python版本和平臺資訊
- **Handoffs 功能**: 模板間智慧跳轉支援
  - 在 clarify、constitution、plan、specify、tasks 命令中新增 handoffs 配置
  - 支援工作流自動化和步驟間跳轉
  - 中文字地化標籤和提示

### 🆕 新增文件和模板
- **升級指南**: 新增完整的升級文件 docs/upgrade.md
  - CLI工具升級步驟
  - 專案檔案更新指南
  - 常見問題和解決方案
  - 版本相容性說明
- **任務轉議題**: 新增 templates/commands/taskstoissues.md
  - 將任務轉換為GitHub議題
  - 支援GitHub MCP伺服器整合
  - 完整的操作流程和警告說明

### 🛠️ 技術增強
- **GitHub API 限制處理**: 增強API限流處理
  - 新增限流頭資訊解析功能
  - 使用者友好的限流錯誤提示
  - 自動重試和等待機制
- **指令碼更新**: 所有構建指令碼同步更新
  - 支援新的 handoffs 功能
  - 改進錯誤處理和日誌
  - PowerShell 指令碼增強

### 🔄 版本管理
- 版本號更新至 0.0.85
- 與原版 v0.0.85 完全同步
- 保持功能對等性

## [0.0.78] - 2025-10-22

### 同步原版
- 同步原版 [v0.0.78](https://github.com/github/spec-kit/releases/tag/v0.0.78)
- 對應原版範圍: v0.0.72 → v0.0.78
- 主要同步提交: `926836e Merge pull request #1001` 等

### 🤖 AI助手支援新增
- **Amp CLI 支援**: 新增對 Amp AI助手的支援
  - 更新 AGENTS.md 新增 Amp CLI 配置
  - 整合到初始化流程: `specify-tw init <project> --ai amp`
  - 更新術語表新增 Amp 條目
  - 完善前置要求和文件說明

### 🛠️ 開發環境增強
- **PowerShell 原生支援**: 新增完整的 Windows 支援
  - 新增 `--script ps` 引數支援
  - 自動指令碼型別檢測（Windows 預設 ps，其他系統預設 sh）
  - 完整的 PowerShell 指令碼整合
- **Devcontainer 支援**: 完整的開發容器配置
  - VS Code Devcontainer 配置同步
  - GitHub Codespaces 支援最佳化
  - 預配置的開發環境設定

### 📚 文件和流程改進
- **本地測試工作流**: 新增詳細的本地測試流程
  - 建立釋出包的完整步驟
  - 本地專案驗證和測試方法
  - 三步驗證流程標準化
- **程式碼品質保證**: 整合 markdownlint-cli2
  - 新增程式碼品質檢查工具
  - 統一的 Markdown 格式規格
  - 自動化品質檢查流程

### 🔧 核心模板更新
- **技術棧支援擴充套件**: implement.md 新增多種技術棧
  - Ruby、PHP、Rust、Kotlin、C++、C、Swift、R 支援
  - Kubernetes/k8s 相關工具模式
  - 更全面的技術棧覆蓋
- **功能增強**: specify.md 新增簡短名稱生成
  - 2-4詞簡短名稱自動生成
  - 完整的生成流程和範例
  - 步驟編號和流程最佳化

### 📖 文件翻譯完善
- **專案級文件**: 全面更新專案文件
  - CONTRIBUTING.md: Devcontainer 和本地測試內容
  - SECURITY.md: 格式標準化和內容最佳化
  - SUPPORT.md: 倉庫連結和引用修正
- **安裝文件**: 更新安裝和快速開始指南
  - PowerShell 支援說明
  - 新增AI助手的安裝指導
  - 命令和連結的同步更新

### 🌐 中文字地化最佳化
- **術語一致性**: 確保所有新功能術語統一
- **連結修正**: 所有GitHub連結指向中文版倉庫
- **使用者體驗**: 保持中文使用者友好的介面和文件

## [0.0.72] - 2025-10-19

### 同步原版
- 同步原版 [v0.0.72](https://github.com/github/spec-kit/releases/tag/v0.0.72)
- 對應原版提交: `3e85f46 Merge pull request #910 from zidoshare/create-new-feature`

### 🚀 重要功能增強
- **VS Code Settings 智慧合併**: `.vscode/settings.json` 現在採用智慧合併而非覆蓋
  - 保留現有使用者設定
  - 新增 Spec Kit 設定項
  - 巢狀物件遞迴合併
  - 防止意外丟失自定義 VS Code 工作區配置

- **IDE代理檢查最佳化**: 最佳化 `check` 命令中的代理檢測邏輯
  - 區分 CLI 和 IDE 型別的 AI 助手
  - IDE 助手跳過 CLI 檢查，標記為可選
  - 更準確的工具鏈檢測結果

### 📝 文件更新
- **README.md**: 新增 AI 助手使用說明提示
- **指令碼修復**: 修復 `create-new-feature.sh` 引數解析問題
- **Agent配置**: 同步最新的AI助手配置資訊

### 🔧 技術改進
- **媒體檔案最佳化**: 減小GIF和圖片檔案體積
- **程式碼品質**: 新增型別提示和程式碼最佳化

## [0.0.69] - 2025-10-16

### 同步原版
- 同步原版 [v0.0.69](https://github.com/github/spec-kit/releases/tag/v0.0.69)
- 對應原版提交: `3b000fc Merge pull request #881 from github/localden/fixes`

### 🔥 關鍵品牌更新
- **CodeBuddy → CodeBuddy CLI**: 同步原版品牌名稱變更
- **安裝連結更新**: CodeBuddy安裝地址從 `https://www.codebuddy.ai` 更新為 `https://www.codebuddy.ai/cli`
- **CLI配置同步**: 更新 `src/specify_cli/__init__.py` 中的AGENT_CONFIG

### 📝 文件格式最佳化
- **README標題統一**: 原版標題大小寫規格化("Get started" → "Get Started")
- **專案描述更新**: 同步原版新的專案描述文字
- **AGENTS.md完整同步**: 包含最新的AI助手整合指南

### 🌐 新增語言支援
- **程式語言擴充套件**: Ruby, PHP, Rust, Kotlin, C, C++
- **模板系統增強**: 支援更多程式語言的專案模板

### 🔧 功能修復
- **命令格式化修正**: 修復代理上下文檔案中的命令格式問題
- **引數處理最佳化**: 改進CLI引數處理邏輯
- **指令碼同步**: 完全同步 `scripts/` 目錄的所有構建指令碼

### 品質驗證
- **CLI功能測試**: 驗證 `specify-tw --help` 和 `specify-tw check` 正常工作
- **CodeBuddy CLI檢測**: 確認工具檢查中正確顯示"CodeBuddy CLI"
- **版本資訊驗證**: 所有版本號已更新至v0.0.69

## [0.0.63] - 2025-10-14

### 同步原版
- 同步原版 [v0.0.63](https://github.com/github/spec-kit/releases/tag/v0.0.63)
- 對應原版提交: `e7bb98de42ef10fc36f2b2f01f17a7c70b92d29a`

### 核心功能修復
- **🔧 CodeBuddy路徑修復**: 修復CodeBuddy AI助手的配置檔案路徑從 `.codebuddy/rules/specify-rules.md` 更改為根目錄的 `CODEBUDDY.md`
- **指令碼同步更新**: 同步 `scripts/bash/update-agent-context.sh` 和 `scripts/powershell/update-agent-context.ps1`
- **Agent整合最佳化**: 確保CodeBuddy助手能夠正確找到和讀取配置檔案

### 文件更新
- **📚 README.md全面同步**: 與原版v0.0.63保持完全一致
- **版本資訊更新**: 對應原版版本從v0.0.62更新至v0.0.63
- **新增升級命令**: 新增 `uv tool install specify-tw-cli --force` 升級說明
- **流程文件完善**: 新增STEP 6詳細說明 `/speckit.tasks` 任務分解流程
- **命令結構最佳化**: 斜槓命令重新分類為"核心命令"和"可選命令"
- **步驟編號調整**: 原STEP 6調整為STEP 7, 插入新的任務分解步驟

### 新增內容
- **🆕 任務分解流程**: 詳細的 `/speckit.tasks` 命令說明, 包含: 
  - 按使用者故事組織的任務分解
  - 依賴管理和並行執行標記
  - 檔案路徑規格和TDD結構
  - 檢查點驗證機制
- **🆕 升級指導**: 提供明確的工具升級命令和說明
- **🆕 命令分類**: 核心命令(5個)和可選命令(3個)的清晰分類

### 技術同步
- **指令碼檔案同步**: Bash和PowerShell指令碼與原版完全同步
- **路徑配置修復**: CodeBuddy配置檔案路徑簡化, 提高可訪問性
- **CLI功能驗證**: 所有AI助手整合功能正常工作

### Bug修復
- **🐛 修復CodeBuddy整合問題**: 解決因路徑錯誤導致的CodeBuddy助手無法正常工作的問題
- **🐛 文件一致性修復**: 確保中文版文件與原版功能描述完全一致

### 已知問題
- 無重大已知問題, 所有功能正常工作

## [0.0.62] - 2025-10-13

### 同步原版
- 同步原版 [v0.0.62](https://github.com/github/spec-kit/releases/tag/v0.0.62)
- 對應原版提交: `e65660f...`(完整包含v0.0.58到v0.0.62的所有變更)

### 核心功能更新
- **Agent配置系統重構**: 從簡單的AI_CHOICES改為結構化的AGENT_CONFIG, 支援更詳細的代理元資料管理
- **新增CodeBuddy AI助手支援**: 完整的CLI工具整合, 支援命令和配置檔案生成
- **Cursor名稱標準化**: 從`cursor`更改為`cursor-agent`, 確保與實際CLI工具名稱一致
- **忽略檔案自動驗證功能**: 在implement命令中新增智慧專案設定驗證, 支援多種技術棧的忽略檔案自動建立
- **Git錯誤高亮顯示**: Git初始化失敗時現在會顯示詳細的錯誤面板, 包含具體的錯誤資訊和修復建議
- **TOML輸出轉義修復**: 修復Gemini CLI中反斜槓轉義問題, 確保配置檔案格式正確

### 中文字地化更新
- **CLI輸出完全中文化**: 所有錯誤訊息、狀態提示、互動介面均保持中文顯示
- **模板檔案中文翻譯**: implement.md新增的忽略檔案驗證功能完全中文化
- **AGENTS.md文件更新**: 同步最新的代理整合指南, 保持技術準確性的同時提供中文說明
- **品牌標識一致性**: 保持中文版特有的品牌標識和命令名稱(specify-tw)

### 構建和指令碼更新
- **構建指令碼完全同步**: 所有bash和PowerShell指令碼與原版保持同步
- **代理上下文更新工具**: 支援新增的CodeBuddy和修正後的cursor-agent
- **VS Code設定模板**: 同步最新的配置選項和快捷鍵支援

### Bug修復
- **🐛 修復speckit.字首缺失問題**: 修復了`.github/workflows/scripts/create-release-packages.sh`中命令檔案生成時缺少`speckit.`字首的關鍵問題, 確保所有AI助手的命令檔案正確生成(如`speckit.analyze.md`而非`analyze.md`)
- **命令相容性恢復**: 修復後用戶可以正常使用`/speckit.constitution`、`/speckit.specify`等命令, 與CLI顯示的命令提示完全匹配

### 已知問題
- 無重大已知問題, 所有功能正常工作

## [0.0.58] - 2025-01-09

### 同步原版
- 同步原版 [v0.0.58](https://github.com/github/spec-kit/releases/tag/v0.0.58)
- 對應原版提交: 多個提交(詳見git log v0.0.55..v0.0.58)
- 主要提交: 
  - `de1db34` - feat(agent): Added Amazon Q Developer CLI Integration
  - `af2b14e` - Add escaping guidelines to command templates
  - `ba8144d` - Package up VS Code settings for Copilot
  - `4dc4887` - Update templates/tasks-template.md
  - `a6be9be` - Update checklist.md

### 新增功能
- ✨ Amazon Q Developer CLI 支援(新增 AI 助手)
- ✨ Checklist 功能: 新增 `/speckit.checklist` 命令用於需求品質驗證
- ✨ VS Code 設定模板: 為 GitHub Copilot 使用者提供配置支援
- 🔧 命令模板轉義指南: 處理特殊字元的標準化方法

### 中文字地化更新
- 完整中文翻譯所有新增內容
- 最佳化現有模板的中文表達
- 更新 CLI 輸出中文介面
- 本地化 checklist-template.md 模板

### 已知問題
- Amazon Q Developer CLI 不支援自定義引數(原版限制)

## [0.0.55] - 2025-10-02

### 同步原版
- 同步原版 [v0.0.55](https://github.com/github/spec-kit/releases/tag/v0.0.55)
- 對應原版提交: `e3b456c` (包含13個功能增強和bug修復提交)
- 主要提交: 
  - `68eba52` - feat: support 'specify init .' for current directory initialization
  - `721ecc9` - feat: Add emacs-style up/down keys
  - `6a3e81f` - docs: fix the paths of generated files (moved under a `.specify/` folder)
  - `b2f749e` - fix: add UTF-8 encoding to file read/write operations in update-agent-context.ps1
  - `cc75a22` - Update URLs to Contributing and Support Guides in Docs

### 新增功能
- **新增 `specify init .` 支援**: 可以使用 `.` 作為當前目錄初始化的簡寫, 等同於 `--here` 標誌但更直觀
- **Emacs 風格快捷鍵**: 新增 Ctrl+P (上) 和 Ctrl+N (下) 鍵盤支援
- **專案檔案結構更新**: 生成的檔案現在統一放在 `.specify/` 目錄下

### 修復
- **UTF-8 編碼支援**: 修復 PowerShell 指令碼中的檔案讀寫編碼問題
- **文件連結修正**: 更新貢獻指南和支援指南的連結地址

### 中文字地化更新
- 更新 README.md 中的命令列引數說明和範例
- 完善所有新增功能的使用範例和中文說明
- 更新專案結構描述, 反映 `.specify/` 目錄變更

### 已知問題
- 無

## [未釋出]

### 新增
- 初始中文版本釋出

### 變更
- 將所有文件從英文翻譯為中文
- 更新命令引用從`specify`改為`specify-tw`

### 修復
- 修復文件中的連結引用

## [1.0.0] - 2024-09-16

### 新增
- 初始版本釋出

## [1.0.54] - 2025-09-28

### 同步原版
- 同步原版 [v0.0.54](https://github.com/github/spec-kit/releases/tag/v0.0.54)
- 對應原版提交: `1c0e7d14d5d5388fbb98b7856ce9f486cc273997`

### 中文字地化更新
- 更新 README.md 中的版本資訊和原版對應關係
- 更新 `src/specify_cli/__init__.py` 檔案, 從原版 spec-kit 專案複製並完全本地化
- 品牌標識更新: 包名 `specify-tw-cli`, 命令名 `specify-tw`, GitHub 倉庫 `rackliu/spec-kit-tw`
- 使用者介面完全中文化: 所有錯誤訊息、狀態提示、幫助文件、操作指導均已翻譯為中文
- 功能完整性驗證: 核心 CLI 功能與原版完全對等, 11 種 AI 助手支援完全一致

### 技術架構同步
- 核心程式碼架構: 所有類和函式名稱、方法簽名、演算法邏輯與原版保持一致
- 依賴管理: typer、rich、httpx 等依賴庫版本與原版同步
- 構建配置: hatchling 構建系統配置保持同步
- AI 助手支援: Claude Code、Gemini CLI、GitHub Copilot、Cursor、Qwen Code 等 11 種助手完全支援

### 已知問題
- 無
- Spec-Driven Development方法論完整實現
- CLI工具支援
- 模板系統
- 文件生成功能
