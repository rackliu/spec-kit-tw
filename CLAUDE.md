# Spec Kit TW

> **專案性質**: GitHub Spec Kit 的官方中文復刻版本, 僅做中文字地化, 不開發新特性

## 專案標識

### 核心資訊
- **專案名稱**: Spec Kit TW
- **原版專案**: [github/spec-kit](https://github.com/github/spec-kit)
- **當前專案**: [rackliu/spec-kit-tw](https://github.com/rackliu/spec-kit-tw)
- **包名**: `specify-tw`(原版: `specify-cli` 不做更改)
- **命令**: `specify-tw`(原版: `specify`)
- **文件語言**: 中文(原版: 英文)

### 核心原則
1. **功能對等**: 與原版保持完全一致的功能, 不新增新特性
2. **僅做本地化**: 專注於中文翻譯和本地化適配
3. **同步優先**: 定期與原版同步, 保持技術更新

### 關鍵差異
| 專案     | 原版            | 中文版           |
| -------- | --------------- | ---------------- |
| 包名     | `specify-cli`   | `specify-tw-cli` |
| 命令     | `specify`       | `specify-tw`     |
| 文件     | 英文            | 中文             |
| 功能     | 持續開發        | 僅做本地化       |
| 斜槓命令 | `/speckit.plan` | 保持一致         |

---

## 快速參考

### 常用命令
```bash
# 開發環境
uv sync                              # 同步依賴
uv run specify-tw --help             # 執行 CLI
uv run specify-tw check              # 檢查工具鏈

# 測試功能
specify-tw init test-project --ai claude    # 測試專案初始化
specify-tw --help | grep -E "中文|Spec Kit TW"  # 驗證中文輸出
```

### 自動化翻譯工作流
```bash
# 一鍵自動化翻譯(推薦)
/translation-auto      # 全自動翻譯流程

# 原版更新處理
/translation-sync      # 智慧同步原版更新

# 品質管理
/translation-qa        # 品質保證檢查
/translation-fix       # 智慧修復問題

# 人工稽核
/translation-review    # 人工稽核(已存在)
/translation-workflow  # 工作流指南
```

### 專案目錄結構
```
專案根目錄/
├── src/specify_cli/           # 核心程式碼(必須同步)
├── templates/                 # 模板檔案(需要本地化)
├── scripts/                   # 構建指令碼(完全同步, 不翻譯)
├── .devcontainer/             # 開發容器配置(完全同步, 不翻譯)
├── .github/                   # CI配置(謹慎同步, 不翻譯)
├── docs/                     # 專案文件(需要本地化)
├── memory/                    # 專案章程(需要本地化)
├── spec-kit/                 # 原版專案(.gitignore)
├── .claude/commands/         # 翻譯自動化命令
├── TERMINOLOGY.md            # 術語表
├── TRANSLATION_STANDARDS.md  # 翻譯標準
├── CHANGELOG.md              # 版本記錄(獨立維護)
└── CLAUDE.md                 # 專案記憶檔案
```

### 檔案分類與處理策略
| 類別       | 目錄/檔案                     | 同步策略 | 本地化策略          |
| ---------- | ----------------------------- | -------- | ------------------- |
| 核心程式碼   | `src/specify_cli/`            | 必須同步 | CLI輸出資訊需要中文 |
| 模板系統   | `templates/`                  | 結構同步 | 完全中文翻譯        |
| 構建指令碼   | `scripts/`                    | 完全同步 | 不翻譯              |
| 開發環境   | `.devcontainer/`              | 完全同步 | 不翻譯              |
| CI配置     | `.github/`                    | 謹慎同步 | 不翻譯              |
| 專案文件   | `docs/`, `README.md`          | 結構參考 | 完全中文翻譯        |
| 專案章程   | `memory/constitution.md`      | 結構同步 | 完全中文翻譯        |
| 原版追蹤   | `spec-kit/`                   | 不提交   | 不適用              |
| 專案描述   | `AGENTS.md`                   | 完全同步 | 不翻譯              |

---

## 技術架構

### 核心元件

#### Specify CLI 結構 (`src/specify_cli/__init__.py`)
**主要類和函式**: 
- `StepTracker` - 分層步驟進度跟蹤 UI 元件
- `select_with_arrows()` - 互動式箭頭鍵選擇介面
- `download_template_from_github()` - GitHub releases 模板下載
- `download_and_extract_template()` - 模板下載和解壓
- `init()` - 主要專案初始化命令
- `check()` - 工具可用性檢查

**關鍵特性**: 
- 支援多種 AI 編碼助手
- 即時進度跟蹤和樹形顯示
- 跨平臺支援(Linux/macOS/Windows)
- 自動指令碼許可權設定(POSIX)
- Git 倉庫自動初始化

### 同步策略
**核心策略**: 採用"**核心同步, 介面本地化**"的策略, 確保與原版功能完全對等的同時, 為中文使用者提供友好的母語介面.

#### 必須同步的內容
- ✅ **所有類和函式名稱**
- ✅ **方法簽名和引數**: 完全與原版一致, 確保功能對等
- ✅ **核心演算法邏輯**: 模板下載、解壓、Git初始化等核心流程
- ✅ **依賴庫和版本**: typer、rich、httpx 等依賴保持同步
- ✅ **AI助手支援**: 所有AI助手的支援邏輯完全一致
- ✅ **構建配置**: hatchling 構建系統保持同步

#### 需要本地化的內容
- 📝 **品牌標識**: 包名、命令名、GitHub倉庫、橫幅標語
- 📝 **使用者介面文字**: 錯誤訊息、狀態提示、互動介面
- 📝 **幫助文件**: 使用說明、操作指導、除錯資訊
- 📝 **輸出資訊**: CLI 輸出、進度顯示、工具檢查結果

### AI 助手支援
| 助手           | CLI 工具       | 目錄格式               | 命令格式 | 型別   |
| -------------- | -------------- | ---------------------- | -------- | ------ |
| Claude Code    | `claude`       | `.claude/commands/`    | Markdown | CLI    |
| Gemini CLI     | `gemini`       | `.gemini/commands/`    | TOML     | CLI    |
| GitHub Copilot | 無(IDE 整合) | `.github/prompts/`     | Markdown | IDE    |
| Cursor         | `cursor-agent` | `.cursor/commands/`    | Markdown | CLI    |
| Qwen Code      | `qwen`         | `.qwen/commands/`      | TOML     | CLI    |
| opencode       | `opencode`     | `.opencode/command/`   | Markdown | CLI    |
| Windsurf       | 無(IDE 整合) | `.windsurf/workflows/` | Markdown | IDE    |
| Codex          | `codex`        | `.codex/`              | Markdown | CLI    |
| Kilocode       | `kilocode`     | `.kilocode/`           | Markdown | CLI    |
| Auggie         | `auggie`       | `.auggie/`             | Markdown | CLI    |
| Amazon Q Developer CLI | `q` | `.amazonq/prompts/` | Markdown | CLI    |

---

## 開發環境配置 (.devcontainer/)

### Devcontainer 概述
`.devcontainer/` 目錄是 v0.0.78 新增的開發容器配置，提供完整的開發環境自動化設定。

### 設定檔結構
```
.devcontainer/
├── devcontainer.json     # 主設定檔，定義容器環境和工具
└── post-create.sh       # 容器建立後自動執行指令碼
```

### 核心功能
- **預配置開發環境**: Python 3.13 + uv 包管理器
- **AI助手自動安裝**: 自動安裝所有支援的AI編碼助手
- **VS Code整合**: 預裝必要的擴充套件和設定
- **多語言支援**: Node.js, .NET, Git 等開發工具
- **埠轉發**: 8080埠用於文件站點預覽

### 包含的AI助手
- GitHub Copilot CLI
- Claude Code CLI
- Codex CLI
- Gemini CLI
- Auggie CLI
- Qwen Code CLI
- OpenCode CLI
- Amazon Q Developer CLI
- CodeBuddy CLI

### 使用方式
1. 在 VS Code 中開啟專案
2. 提示"在容器中重新開啟"時選擇確定
3. 等待容器構建和指令碼執行完成
4. 所有AI助手將自動安裝並可用

### 同步策略
- **完全同步**: 與原版保持100%一致
- **不翻譯**: 所有設定檔保持英文
- **自動更新**: 隨原版版本同步更新

---

## 維護工作流程

### 自動化翻譯工作流

#### 推薦使用流程
1. **首次設定**: `/translation-auto` 執行完整翻譯
2. **原版更新**: `/translation-sync` 智慧同步更新
3. **日常維護**: `/translation-qa` + `/translation-fix` 品質管理
4. **釋出檢查**: `/translation-review` 最終稽核

#### 工作流特性
- **90%+ 自動化**: 大幅減少人工干預
- **智慧檢測**: 自動識別翻譯需求和品質問題
- **增量更新**: 僅處理變更內容, 保持現有翻譯穩定
- **品質保證**: 多層檢查確保翻譯品質
- **安全機制**: 分支操作、自動備份、漸進式釋出

### 版本同步策略

#### 基本原則
- **版本號**: 本專案tag單獨迭代, 不需要和原版同步
- **功能同步**: 定期從上游合併, 不新增新功能
- **釋出節奏**: 跟隨原版釋出, 不獨立釋出新功能

#### 同步機制
**spec-kit 目錄工作機制**: 
```
專案根目錄/
├── spec-kit/              # 原版專案目錄(.gitignore)
│   ├── .git/             # 原版 git 歷史
│   ├── src/              # 原版原始碼
│   ├── templates/        # 原版模板
│   └── ...
├── .gitignore            # 忽略 spec-kit/ 目錄
└── ...                   # 本專案檔案
```

**同步工作流程**:
1. 檢查當前版本對應的原版 tag/commit
2. 在 `spec-kit/` 目錄檢出對應原版版本
3. 完全同步scripts: `rsync -avp spec-kit/scripts/ scripts/`
4. **關鍵步驟**: 同步AGENTS.md: `cp spec-kit/AGENTS.md AGENTS.md`
5. 同步開發環境配置: `rsync -avp spec-kit/.devcontainer/ .devcontainer/`
6. 執行自動化翻譯: `/translation-sync`
7. 更新 CHANGELOG.md 記錄同步資訊

#### AGENTS.md 比對的重要性
- 原版 `AGENTS.md` 包含最新的 AI 助手支援資訊和技術細節
- 每次同步時必須比對, 確保專案記憶的準確性
- 重點關注: 新助手支援、版本管理要求、整合步驟變化

### 版本管理要求
- **重要**: 任何對 `src/specify_cli/__init__.py` 的修改都需要: 
  - 更新 `pyproject.toml` 中的版本號
  - 在 `CHANGELOG.md` 中新增相應條目
  - 同步原版更新時記錄對應的原版提交資訊

### CHANGELOG 維護
**維護原則**: 
- `CHANGELOG.md` 由本專案獨立維護, 不與原版同步
- 記錄每個版本同步的原版資訊和中文字地化更新

---

## 翻譯標準和品質保證

### 翻譯標準檔案
- **@TRANSLATION_STANDARDS.md**: 詳細的翻譯標準和規格
- **@TERMINOLOGY.md**: 標準術語表, 確保翻譯一致性

### 核心翻譯原則
- **使用者導向**: 面向中文開發者, 翻譯使用者介面和文件
- **技術保留**: 程式碼層面保持英文, 確保技術準確性
- **功能對等**: 翻譯後功能必須與原版完全一致
- **術語一致**: 嚴格遵循術語表, 保持翻譯一致性

### 本地化範圍
**需要完全中文字地化的內容**: 
- 使用者文件: `README.md`、`spec-driven.md`、`docs/` 目錄
- 模板系統: `templates/` 和 `templates/commands/` 目錄下的所有檔案
- 專案章程: `memory/constitution.md`(包括佔位符和說明文字)
- CLI 介面: `src/specify_cli/` 中的輸出資訊、幫助文字、錯誤訊息

**保持英文不翻譯的內容**:
- 構建指令碼: `scripts/` 目錄(完全同步原版)
- 開發環境: `.devcontainer/` 目錄(完全同步原版)
- 媒體資源: `media/` 目錄(完全同步原版)
- CI配置: `.github/` 目錄(謹慎同步, 不翻譯)
- 程式碼層面: 變數名、函式名、類名等識別符號
- 章程佔位符: 如 `[PROJECT_NAME]`、`[PRINCIPLE_1_NAME]` 等(保持原格式)

### 品質保證機制
- **自動化檢查**: `/translation-qa` 進行全面品質檢查
- **智慧修復**: `/translation-fix` 自動修復常見問題
- **人工稽核**: `/translation-review` 最終品質把關
- **持續改進**: 基於使用者反饋持續最佳化翻譯品質

---

## 打包釋出

**釋出觸發**: 推送格式為 `v*.*.*` 的 tag 時自動觸發 GitHub Actions, push 到 main 分支不會觸發.

**版本規則**: Tag 使用 `v0.0.85` 格式, 生成的包名去掉 v 字首為 `spec-kit-template-*-0.0.85.zip`.

**釋出命令**: `git tag v0.0.85 && git push origin v0.0.85` 即可自動建立包含 24 個包的完整 release.

---

## 緊急情況處理

### 常見問題解決方案
1. **同步衝突**: 優先保留原版功能, 僅在本地化內容上保留修改
2. **版本不一致**: 檢查 `pyproject.toml` 和 `CHANGELOG.md`
3. **功能異常**: 對比原版專案, 確認是否為同步問題
4. **翻譯品質問題**: 使用 `/translation-fix` 智慧修復

---

## 參考連結

- **原版專案**: [github/spec-kit](https://github.com/github/spec-kit)
- **原版文件**: [spec-kit/docs](https://github.com/github/spec-kit/tree/main/docs)
- **原版專案標書**: [spec-kit/AGENTS.md](https://github.com/github/spec-kit/blob/main/AGENTS.md)
- **GitHub Releases**: [spec-kit/releases](https://github.com/github/spec-kit/releases)
- **中文版倉庫**: [rackliu/spec-kit-tw](https://github.com/rackliu/spec-kit-tw)
- **翻譯標準**: @TRANSLATION_STANDARDS.md
- **術語表**: @TERMINOLOGY.md

## 其他Rule

- 原版專案位於`./spec-kit`, 如果沒有, 就將它克隆到這個位置, 始終從該位置訪問原版檔案
- 同步src下指令碼檔案時, 務必將repo_name和repo_user替換為本專案的
- 記得在提交程式碼前更新README.md中的版本資訊
