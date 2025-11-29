<div align="center">
    <img src="./media/logo_small.webp" alt="Spec Kit Logo"/>
    <h1>🌱 Spec Kit TW</h1>
    <h3><em>更快地構建高品質軟體. </em></h3>
</div>

<p align="center">
    <strong>這是一項旨在幫助組織專注於產品場景而非編寫無差異化程式碼的努力, 藉助規格驅動開發(Spec-Driven Development)的力量. </strong>
</p>

<p align="center">
    <a href="https://github.com/rackliu/spec-kit-tw/actions/workflows/release.yml"><img src="https://github.com/rackliu/spec-kit-tw/actions/workflows/release.yml/badge.svg" alt="Release"/></a>
    <a href="https://github.com/rackliu/spec-kit-tw/stargazers"><img src="https://img.shields.io/github/stars/rackliu/spec-kit-tw?style=social" alt="GitHub stars"/></a>
    <a href="https://github.com/rackliu/spec-kit-tw/blob/main/LICENSE"><img src="https://img.shields.io/github/license/rackliu/spec-kit-tw" alt="License"/></a>
    <a href="https://rackliu.github.io/spec-kit-tw/"><img src="https://img.shields.io/badge/docs-GitHub_Pages-blue" alt="Documentation"/></a>
</p>

> **💡 這是 [GitHub Spec Kit](https://github.com/github/spec-kit) 的官方中文復刻版本**
> ** 部分內容來自：https://github.com/doggy8088/spec-kit
> 
> **🔄 對應原版版本**: [v0.0.85](https://github.com/github/spec-kit/releases/tag/v0.0.85)
> 
> **📦 包名**: `specify-tw-cli`
>
>  **🛠️ 命令**: `specify-tw`
>
> **⚠️ 保持同步**: 本專案將定期與原版保持同步, 確保中文使用者能夠享受最新的功能和改進.

---

## 目錄

- [目錄](#目錄)
  - [🎯 差異說明](#-差異說明)
- [🤔 什麼是規格驅動開發？](#-什麼是規格驅動開發)
- [⚡ 快速開始](#-快速開始)
  - [1. 安裝 Specify TW](#1-安裝-specify-tw)
    - [方式 1: 持久化安裝(推薦)](#方式-1-持久化安裝推薦)
    - [方式 2: 一次性使用](#方式-2-一次性使用)
  - [2. 建立專案原則](#2-建立專案原則)
  - [3. 建立規格](#3-建立規格)
  - [4. 建立技術實施計劃](#4-建立技術實施計劃)
  - [5. 分解任務](#5-分解任務)
  - [6. 執行實施](#6-執行實施)
- [📽️ 影片概述](#️-影片概述)
- [🤖 支援的 AI 代理](#-支援的-ai-代理)
- [🔧 Specify TW CLI 參考](#-specify-tw-cli-參考)
  - [命令](#命令)
  - [`specify-tw init` 引數和選項](#specify-tw-init-引數和選項)
  - [範例](#範例)
  - [可用的斜槓命令](#可用的斜槓命令)
    - [核心命令](#核心命令)
    - [可選命令](#可選命令)
  - [環境變數](#環境變數)
- [📚 核心理念](#-核心理念)
- [🌟 開發階段](#-開發階段)
- [🎯 實驗目標](#-實驗目標)
  - [技術獨立性](#技術獨立性)
  - [企業約束](#企業約束)
  - [以使用者為中心的開發](#以使用者為中心的開發)
  - [創意和迭代過程](#創意和迭代過程)
- [🔧 前置要求](#-前置要求)
- [📖 瞭解更多](#-瞭解更多)
- [📋 詳細流程](#-詳細流程)
  - [步驟1:  建立專案原則](#步驟1--建立專案原則)
  - [步驟2:  建立專案規格](#步驟2--建立專案規格)
  - [步驟3:  功能規格澄清(計劃前必需)](#步驟3--功能規格澄清計劃前必需)
  - [步驟4:  生成計劃](#步驟4--生成計劃)
  - [步驟5:  讓Claude Code驗證計劃](#步驟5--讓claude-code驗證計劃)
  - [步驟6:  使用 /speckit.tasks 生成任務分解](#步驟6--使用-speckittasks-生成任務分解)
  - [步驟7:  實施](#步驟7--實施)
- [🔍 故障排除](#-故障排除)
  - [Linux上的Git憑據管理器](#linux上的git憑據管理器)
- [👥 維護者](#-維護者)
- [💬 支援](#-支援)
- [🙏 致謝](#-致謝)
- [📄 許可證](#-許可證)


### 🎯 差異說明

| 專案 | Spec Kit原版  | Spec Kit TW中文版 |
| ---- | ------------- | ----------------- |
| 命令 | `specify`     | `specify-tw`      |
| 包名 | `specify-cli` | `specify-tw-cli`  |
| 文件 | 英文          | 中文              |

---

## 🤔 什麼是規格驅動開發？

規格驅動開發**徹底顛覆**了傳統軟體開發的方式. 幾十年來, 程式碼一直佔據主導地位——規格只是我們在編碼"真正工作"開始時構建和丟棄的鷹架. 規格驅動開發改變了這一點: **規格變得可執行**, 直接生成可工作的實現, 而不僅僅是指導它們.

## ⚡ 快速開始

### 1. 安裝 Specify TW

選擇你偏好的安裝方式: 

#### 方式 1: 持久化安裝(推薦)

一次安裝, 隨處使用: 

```bash
uv tool install specify-tw-cli --from git+https://github.com/rackliu/spec-kit-tw.git
```

然後直接使用工具: 

```bash
specify-tw init <PROJECT_NAME>
specify-tw check
```

要升級 specify-tw, 執行: 

```bash
uv tool install specify-tw-cli --force --from git+https://github.com/rackliu/spec-kit-tw.git
```

#### 方式 2: 一次性使用

直接執行, 無需安裝: 

```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <PROJECT_NAME>
```

**持久化安裝的優勢**:

- 工具保持安裝狀態並在 PATH 中可用
- 無需建立 shell 別名
- 更好的工具管理: `uv tool list`、`uv tool upgrade`、`uv tool uninstall`
- 更簡潔的 shell 配置

### 2. 建立專案原則

在專案目錄中啟動你的 AI 助手。助手可使用 `/speckit.*` 命令。

使用 **`/speckit.constitution`** 命令建立專案的指導原則和開發指南, 這將指導所有後續開發.

```bash
/speckit.constitution 建立專注於程式碼品質、測試標準、使用者體驗一致性和效能要求的原則
```

### 3. 建立規格

使用 **`/speckit.specify`** 命令描述你想要構建的內容. 專注於**做什麼**和**為什麼**, 而不是技術棧.

```bash
/speckit.specify 構建一個可以幫助我將照片整理到不同相簿中的應用程式. 相簿按日期分組, 可以透過在主頁上拖拽來重新組織. 相簿不會巢狀在其他相簿中. 在每個相簿內, 照片以瓷磚介面預覽.
```

### 4. 建立技術實施計劃

使用 **`/speckit.plan`** 命令提供你的技術棧和架構選擇.

```bash
/speckit.plan 應用程式使用 Vite 和最少數量的庫. 儘可能使用純 HTML、CSS 和 JavaScript. 圖片不會上傳到任何地方, 元資料儲存在本地 SQLite 資料庫中.
```

### 5. 分解任務

使用 **`/speckit.tasks`** 從你的實施計劃建立可操作的任務列表.

```bash
/speckit.tasks
```

### 6. 執行實施

使用 **`/speckit.implement`** 執行所有任務並根據計劃構建你的功能.

```bash
/speckit.implement
```

詳細的分步說明, 請參閱我們的[綜合指南](./spec-driven.md).

## 📽️ 影片概述

想要觀看 Spec Kit 的實際操作？觀看我們的[影片概述](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)! 

[![Spec Kit 影片標題](/media/spec-kit-video-header.jpg)](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)

## 🤖 支援的 AI 代理

| 代理                                                      | 支援 | 說明                                                                               |
| --------------------------------------------------------- | ---- | ---------------------------------------------------------------------------------- |
| [Claude Code](https://www.anthropic.com/claude-code)      | ✅    | Anthropic Claude Code助手                                                           |
| [GitHub Copilot](https://code.visualstudio.com/)          | ✅    | GitHub Copilot IDE整合                                                              |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | ✅    | Google Gemini CLI助手                                                               |
| [Cursor](https://cursor.sh/)                              | ✅    | Cursor AI編輯器                                                                     |
| [Qwen Code](https://github.com/QwenLM/qwen-code)          | ✅    | 阿里雲通義千問程式碼助手                                                              |
| [opencode](https://opencode.ai/)                          | ✅    | opencode AI助手                                                                     |
| [Windsurf](https://windsurf.com/)                         | ✅    | Windsurf AI編輯器                                                                   |
| [Kilo Code](https://github.com/Kilo-Org/kilocode)         | ✅    | Kilo Code AI助手                                                                    |
| [Auggie CLI](https://docs.augmentcode.com/cli/overview)   | ✅    | Auggie CLI助手                                                                      |
| [Roo Code](https://roocode.com/)                          | ✅    | Roo Code AI助手                                                                     |
| [CodeBuddy](https://www.codebuddy.ai/)                    | ✅    | CodeBuddy AI助手                                                                    |
| [Codex CLI](https://github.com/openai/codex)              | ✅    | OpenAI Codex CLI助手                                                                |
| [Amazon Q Developer CLI](https://aws.amazon.com/developer/learning/q-developer-cli/) | ⚠️ | Amazon Q Developer CLI [不支援](https://github.com/aws/amazon-q-developer-cli/issues/3064) 斜槓命令的自定義引數.  |
| [Amp](https://ampcode.com/)                               | ✅    | Amp AI助手                                                                          |

## 🔧 Specify TW CLI 參考

`specify-tw` 命令支援以下選項: 

### 命令

| 命令    | 描述                                                                                                                          |
| ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `init`  | 從最新模板初始化新的 Specify TW 專案                                                                                          |
| `check` | 檢查已安裝的工具 (`git`, `claude`, `gemini`, `code`/`code-insiders`, `cursor-agent`, `windsurf`, `qwen`, `opencode`, `codex`, `q`) |

### `specify-tw init` 引數和選項

| 引數/選項              | 型別 | 描述                                                                                                                             |
| ---------------------- | ---- | -------------------------------------------------------------------------------------------------------------------------------- |
| `<project-name>`       | 引數 | 新專案目錄的名稱(使用 `--here` 時可選, 或使用 `.` 表示當前目錄)                                                                                         |
| `--ai`                 | 選項 | 要使用的 AI 助手: `claude`, `gemini`, `copilot`, `cursor-agent`, `qwen`, `opencode`, `codex`, `windsurf`, `kilocode`, `auggie`, `roo`, `codebuddy`, `amp`, 或 `q` |
| `--script`             | 選項 | 要使用的指令碼變體: `sh` (bash/zsh) 或 `ps` (PowerShell)                                                                           |
| `--ignore-agent-tools` | 標誌 | 跳過 AI 代理工具的檢查, 如 Claude Code                                                                                             |
| `--no-git`             | 標誌 | 跳過 git 倉庫初始化                                                                                                              |
| `--here`               | 標誌 | 在當前目錄初始化專案, 而不是建立新目錄                                                                                           |
| `--force`              | 標誌 | 在當前目錄中初始化時強制合併/覆蓋(跳過確認)                                                                                    |
| `--skip-tls`           | 標誌 | 跳過 SSL/TLS 驗證(不推薦)                                                                                                      |
| `--debug`              | 標誌 | 啟用詳細除錯輸出以進行故障排除                                                                                                   |
| `--github-token`       | 選項 | API 請求的 GitHub 令牌(或設定 GH_TOKEN/GITHUB_TOKEN 環境變數)                                                                  |

### 範例

```bash
# 基本專案初始化
specify-tw init my-project

# 使用特定AI助手初始化
specify-tw init my-project --ai claude

# 使用 Cursor 支援初始化
specify-tw init my-project --ai cursor-agent

# 使用 Windsurf 支援初始化
specify-tw init my-project --ai windsurf

# 使用 Amp 支援初始化
specify-tw init my-project --ai amp

# 使用 PowerShell 指令碼初始化(Windows/跨平臺)
specify-tw init my-project --ai copilot --script ps

# 在當前目錄初始化
specify-tw init . --ai copilot
# 或使用 --here 標誌
specify-tw init --here --ai copilot

# 強制合併到當前(非空)目錄而無需確認
specify-tw init . --force --ai copilot
# 或
specify-tw init --here --force --ai copilot

# 跳過 git 初始化
specify-tw init my-project --ai gemini --no-git

# 啟用除錯輸出以進行故障排除
specify-tw init my-project --ai claude --debug

# 使用 GitHub 令牌進行 API 請求(對企業環境有幫助)
specify-tw init my-project --ai claude --github-token ghp_your_token_here

# 檢查系統要求
specify-tw check
```

### 可用的斜槓命令

執行 `specify-tw init` 後, 你的AI編碼代理將可以使用這些斜槓命令進行結構化開發: 

#### 核心命令

規格驅動開發工作流的基本命令: 

| 命令                  | 描述                                                           |
| --------------------- | ------------------------------------------------------------- |
| `/speckit.constitution`  | 建立或更新專案指導原則和開發指南                               |
| `/speckit.specify`       | 定義你想要構建的內容(需求和使用者故事)                         |
| `/speckit.plan`          | 使用你選擇的技術棧建立技術實施計劃                             |
| `/speckit.tasks`         | 為實施生成可操作的任務列表                                     |
| `/speckit.implement`     | 執行所有任務以根據計劃構建功能                                 |

#### 可選命令

用於增強品質和驗證的附加命令:

| 命令              | 描述                                                           |
| ------------------ | ------------------------------------------------------------- |
| `/speckit.clarify`   | 澄清未充分說明的區域(建議在 `/speckit.plan` 之前執行; 以前為 `/quizme`) |
| `/speckit.analyze`   | 跨製品一致性和覆蓋範圍分析(在 /speckit.tasks 之後, /speckit.implement 之前執行) |
| `/speckit.checklist` | 生成自定義品質檢查清單, 驗證需求的完整性、清晰性和一致性(類似"英文的單元測試") |

### 環境變數

| 變數              | 描述                                                                                                                                                                                           |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SPECIFY_FEATURE` | 為非 Git 倉庫覆蓋功能檢測. 設定為功能目錄名稱(例如, `001-photo-albums`)以在不使用 Git 分支的情況下處理特定功能. <br/>**必須在你正在使用的代理上下文中設定, 然後才能使用 `/speckit.plan` 或後續命令.  |

## 📚 核心理念

規格驅動開發是一個強調以下方面的結構化過程: 

- **意圖驅動開發**, 規格在"如何"之前定義"什麼"
- **豐富的規格建立**, 使用護欄和組織原則
- **多步細化**, 而不是從提示一次性生成程式碼
- **高度依賴**高階AI模型能力進行規格解釋

## 🌟 開發階段

| 階段 | 重點 | 關鍵活動 |
|-------|-------|----------------|
| **0到1開發**("新建專案") | 從頭生成 | <ul><li>從高層需求開始</li><li>生成規格</li><li>規劃實施步驟</li><li>構建生產就緒的應用程式</li></ul> |
| **創意探索** | 並行實現 | <ul><li>探索多樣化的解決方案</li><li>支援多種技術棧和架構</li><li>實驗UX模式</li></ul> |
| **迭代增強**("現有專案改造") | 現有專案現代化 | <ul><li>迭代新增功能</li><li>現代化遺留系統</li><li>適應流程</li></ul> |

## 🎯 實驗目標

我們的研究和實驗專注於: 

### 技術獨立性

- 使用多樣化的技術棧建立應用程式
- 驗證規格驅動開發是一個不依賴於特定技術、程式語言或框架的過程

### 企業約束

- 展示關鍵任務應用程式開發
- 融入組織約束(雲提供商、技術棧、工程實踐)
- 支援企業設計系統和合規要求

### 以使用者為中心的開發

- 為不同使用者群體和偏好構建應用程式
- 支援各種開發方法(從氛圍編碼到AI原生開發)

### 創意和迭代過程

- 驗證並行實現探索的概念
- 提供強大的迭代功能開發工作流
- 擴充套件流程以處理升級和現代化任務

## 🔧 前置要求

- **Linux/macOS**(或Windows上的WSL2)
- AI編碼代理: [Claude Code](https://www.anthropic.com/claude-code)、[GitHub Copilot](https://code.visualstudio.com/)、[Gemini CLI](https://github.com/google-gemini/gemini-cli)、[Cursor](https://cursor.sh/)、[Qwen CLI](https://github.com/QwenLM/qwen-code)、[opencode](https://opencode.ai/)、[Codex CLI](https://github.com/openai/codex)、[Windsurf](https://windsurf.com/)、[Amp](https://ampcode.com/) 或 [Amazon Q Developer CLI](https://aws.amazon.com/developer/learning/q-developer-cli/)
- [uv](https://docs.astral.sh/uv/) 用於包管理
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

如果你在使用代理時遇到問題, 請開啟 issue 以便我們完善整合.

## 📖 瞭解更多

- **[完整的規格驅動開發方法論](./spec-driven.md)** - 深入瞭解完整流程
- **[詳細演練](#-詳細流程)** - 分步實施指南

---

## 📋 詳細流程

<details>
<summary>點選展開詳細的分步演練</summary>

你可以使用Specify TW CLI來引導你的專案, 這將在你的環境中引入所需的製品. 執行: 

```bash
specify-tw init <project_name>
```

或在當前目錄初始化: 

```bash
specify-tw init .
# 或使用 --here 標誌
specify-tw init --here
# 跳過確認當目錄已有檔案時
specify-tw init . --force
# 或
specify-tw init --here --force
```

![Specify TW CLI在終端中引導新專案](./media/specify_cli.gif)

系統會提示你選擇正在使用的AI代理. 你也可以直接在終端中主動指定: 

```bash
specify-tw init <project_name> --ai claude
specify-tw init <project_name> --ai gemini
specify-tw init <project_name> --ai copilot
specify-tw init <project_name> --ai cursor-agent
specify-tw init <project_name> --ai qwen
specify-tw init <project_name> --ai opencode
specify-tw init <project_name> --ai codex
specify-tw init <project_name> --ai windsurf
specify-tw init <project_name> --ai amp
specify-tw init <project_name> --ai kilocode
specify-tw init <project_name> --ai auggie
specify-tw init <project_name> --ai roo
# 或在當前目錄: 
specify-tw init --here --ai claude
specify-tw init --here --ai codex
# 強制合併到非空的當前目錄
specify-tw init --here --force --ai claude
```

CLI會檢查你是否安裝了Claude Code、Gemini CLI、Cursor CLI、Qwen CLI、opencode或Codex CLI. 如果你沒有安裝, 或者你希望在不檢查正確工具的情況下獲取模板, 請在命令中使用 `--ignore-agent-tools`: 

```bash
specify-tw init <project_name> --ai claude --ignore-agent-tools
```

### 步驟1:  建立專案原則

轉到專案資料夾並執行你的AI代理. 在我們的範例中, 我們使用 `claude`.

![引導Claude Code環境](./media/bootstrap-claude-code.gif)

如果你看到 `/speckit.constitution`、`/speckit.specify`、`/speckit.plan`、`/speckit.tasks` 和 `/speckit.implement` 命令可用, 就說明配置正確.

第一步應該是使用 `/speckit.constitution` 命令建立專案的指導原則. 這有助於確保在所有後續開發階段中做出一致的決策:

```text
/speckit.constitution 建立專注於程式碼品質、測試標準、使用者體驗一致性和效能要求的原則. 包括這些原則應如何指導技術決策和實施選擇的治理.
```

此步驟會建立或更新 `.specify/memory/constitution.md` 檔案, 其中包含專案的基礎指南, AI代理將在規格、規劃和實施階段參考這些指南.

### 步驟2:  建立專案規格

有了專案原則後, 你現在可以建立功能規格. 使用 `/speckit.specify` 命令, 然後為你想要開發的專案提供具體需求.

>[!IMPORTANT]
>儘可能明確地說明你要構建的*什麼*和*為什麼*. **此時不要關注技術棧**.

範例提示: 

```text
開發Taskify, 一個團隊生產力平臺. 它應該允許使用者建立專案、新增團隊成員、
分配任務、評論並以看板風格在板之間移動任務. 在此功能的初始階段, 
我們稱之為"建立Taskify", 我們將有多個使用者, 但使用者將提前預定義.
我想要兩個不同類別的五個使用者, 一個產品經理和四個工程師. 讓我們建立三個
不同的範例專案. 讓我們為每個任務的狀態使用標準的看板列, 如"待辦"、
"進行中"、"稽核中"和"已完成". 此應用程式將沒有登入, 因為這只是
確保我們基本功能設定的第一次測試. 對於UI中的任務卡片, 
你應該能夠在看板工作板的不同列之間更改任務的當前狀態.
你應該能夠為特定卡片留下無限數量的評論. 你應該能夠從該任務
卡片中分配一個有效使用者. 當你首次啟動Taskify時, 它會給你一個五個使用者的列表供你選擇.
不需要密碼. 當你點選使用者時, 你進入主檢視, 顯示專案列表.
當你點選專案時, 你會開啟該專案的看板. 你將看到列.
你將能夠在不同列之間來回拖放卡片. 你將看到分配給你的任何卡片, 
即當前登入使用者, 與其他卡片顏色不同, 以便你快速看到你的卡片.
你可以編輯你所做的任何評論, 但不能編輯其他人所做的評論. 你可以
刪除你所做的任何評論, 但不能刪除其他人所做的評論.
```

輸入此提示後, 你應該看到Claude Code啟動規劃和規格起草過程. Claude Code還將觸發一些內建指令碼來設定倉庫.

完成此步驟後, 你應該有一個新建立的分支(例如, `001-create-taskify`), 以及 `specs/001-create-taskify` 目錄中的新規格.

生成的規格應包含一組使用者故事和功能需求, 如模板中所定義.

在此階段, 你的專案資料夾內容應類似於以下內容: 

```text
└── .specify
    ├── memory
    │	 └── constitution.md
    ├── scripts
    │	 ├── check-prerequisites.sh
    │	 ├── common.sh
    │	 ├── create-new-feature.sh
    │	 ├── setup-plan.sh
    │	 └── update-cluade-md.sh
    ├── specs
    │	 └── 001-create-taskify
    │	     └── spec.md
    └── templates
        ├── plan-template.md
        ├── spec-template.md
        └── tasks-template.md
```

### 步驟3:  功能規格澄清(計劃前必需)

建立了基線規格後, 你可以繼續澄清在第一次嘗試中未正確捕獲的任何需求.

你應該在建立技術計劃之前執行結構化澄清工作流程, 以減少下游的返工.

首選順序:
1. 使用 `/speckit.clarify`(結構化)- 順序的、基於覆蓋率的提問, 將答案記錄在澄清部分.
2. 如果仍然感覺模糊, 可以選擇性地進行臨時自由形式細化.

如果你有意跳過細節澄清環節(例如，進行概念驗證或探索性原型設計), 請明確說明, 這樣智慧體就不會因缺少澄清資訊而停滯不前.

一個自由形式的最佳化提示範例(在 `/speckit.clarify` 之後如果仍然需要): 

```text
對於你建立的每個範例專案或專案, 每個專案應該有5到15個之間的可變數量任務, 
隨機分佈到不同的完成狀態. 確保每個完成階段至少有一個任務.
```

你還應該要求Claude Code驗證**稽核和驗收清單**, 勾選驗證/透過要求的專案, 未透過的專案保持未勾選狀態. 可以使用以下提示: 

```text
閱讀稽核和驗收清單, 如果功能規格符合標準, 請勾選清單中的每個專案. 如果不符合, 請留空.
```

重要的是, 要將與Claude Code的互動作為澄清和圍繞規格提問的機會——**不要將其第一次嘗試視為最終版本**.

### 步驟4:  生成計劃

你現在可以具體說明技術棧和其他技術要求. 你可以使用專案模板中內建的 `/speckit.plan` 命令, 使用這樣的提示: 

```text
我們將使用.NET Aspire生成這個, 使用Postgres作為資料庫. 前端應該使用
Blazor伺服器與拖拽任務板、即時更新. 應該建立一個REST API, 包含專案API、
任務API和通知API.
```

此步驟的輸出將包括許多實施細節文件, 你的目錄樹類似於: 

```text
.
├── CLAUDE.md
├── memory
│	 └── constitution.md
├── scripts
│	 ├── check-prerequisites.sh
│	 ├── common.sh
│	 ├── create-new-feature.sh
│	 ├── setup-plan.sh
│	 └── update-cluade-md.sh
├── specs
│	 └── 001-create-taskify
│	     ├── contracts
│	     │	 ├── api-spec.json
│	     │	 └── signalr-spec.md
│	     ├── data-model.md
│	     ├── plan.md
│	     ├── quickstart.md
│	     ├── research.md
│	     └── spec.md
└── templates
    ├── CLAUDE-template.md
    ├── plan-template.md
    ├── spec-template.md
    └── tasks-template.md
```

檢查 `research.md` 文件, 確保根據你的說明使用了正確的技術棧. 如果任何元件突出顯示, 你可以要求Claude Code完善它, 甚至讓它檢查你想要使用的平臺/框架的本地安裝版本(例如, .NET).

此外, 如果你選擇的技術棧是快速變化的(例如, .NET Aspire、JS框架), 你可能想要要求Claude Code研究有關所選技術棧的詳細資訊, 使用這樣的提示: 

```text
我希望你檢視實施計劃和實施細節, 尋找可能從額外研究中受益的領域, 
因為.NET Aspire是一個快速變化的庫. 對於你識別的需要進一步研究的那些領域, 
我希望你使用有關我們將在Taskify應用程式中使用的特定版本的額外詳細資訊更新研究文件, 
並啟動並行研究任務, 使用網路研究澄清任何細節.
```

在此過程中, 你可能會發現Claude Code卡在研究錯誤的內容——你可以使用這樣的提示幫助它朝著正確的方向推進: 

```text
我認為我們需要將其分解為一系列步驟. 首先, 識別你在實施期間需要做的不確定
或從進一步研究中受益的任務列表. 寫下這些任務的列表. 然後對於這些任務中的每一個, 
我希望你啟動一個單獨的研究任務, 這樣最終結果是我們並行研究所有這些非常具體的任務.
我看到你所做的是看起來你在研究.NET Aspire一般情況, 我認為這對我們不會有太大幫助.
那太沒有針對性的研究了. 研究需要幫助你解決特定的針對性問題.
```

>[!NOTE]
>Claude Code可能過於急切, 新增你沒有要求的元件. 要求它澄清變更的理由和來源.

### 步驟5:  讓Claude Code驗證計劃

有了計劃後, 你應該讓Claude Code檢查它, 確保沒有遺漏的部分. 你可以使用這樣的提示: 

```text
現在我希望你去稽核實施計劃和實施細節檔案.
帶著確定是否存在從閱讀中可以明顯看出的你需要做的一系列任務的眼光來閱讀.
因為我不確定這裡是否足夠. 例如, 當我檢視核心實施時, 參考實施細節中的適當位置
會很有用, 以便在它執行核心實施或細化中的每個步驟時可以找到資訊.
```

這有助於完善實施計劃, 並幫助你避免Claude Code在其規劃週期中遺漏的潛在盲點. 一旦初始細化完成, 在你可以進入實施之前, 要求Claude Code再次檢查清單.

你也可以要求Claude Code(如果你安裝了[GitHub CLI](https://docs.github.com/en/github-cli/github-cli))繼續從你當前的分支向 `main` 建立一個詳細描述的pull request, 以確保工作得到正確跟蹤.

>[!NOTE]
>在讓代理實施之前, 還值得提示Claude Code交叉檢查細節, 看看是否有任何過度設計的部分(記住——它可能過於急切). 如果存在過度設計的元件或決策, 你可以要求Claude Code解決它們. 確保Claude Code遵循[專案章程](.specify/memory/constitution.md)作為建立計劃時必須遵守的基礎.

### 步驟6:  使用 /speckit.tasks 生成任務分解

實施計劃驗證通過後, 你現在可以將計劃分解為具體的、可執行的任務, 這些任務可以按正確的順序執行. 使用 `/speckit.tasks` 命令從你的實施計劃自動生成詳細的任務分解:

```text
/speckit.tasks
```

此步驟會在你的功能規格目錄中建立一個 `tasks.md` 檔案, 其中包含: 

- **按使用者故事組織的任務分解** - 每個使用者故事成為一個獨立的實施階段, 包含自己的任務集
- **依賴管理** - 任務按依賴關係排序, 尊重元件間的依賴(例如, 模型在服務之前, 服務在端點之前)
- **並行執行標記** - 可以並行執行的任務用 `[P]` 標記, 以最佳化開發工作流
- **檔案路徑規格** - 每個任務包含實施應發生的確切檔案路徑
- **測試驅動開發結構** - 如果要求測試, 則包含測試任務並排序為在實施之前編寫
- **檢查點驗證** - 每個使用者故事階段包含檢查點以驗證獨立功能

生成的 tasks.md 為 `/speckit.implement` 命令提供了清晰的路線圖, 確保系統性實施, 保持程式碼品質並允許使用者故事的增量交付.

### 步驟7:  實施

準備就緒後, 使用 `/speckit.implement` 命令執行你的實施計劃:

```text
/speckit.implement
```

`/speckit.implement` 命令將: 
- 驗證所有先決條件都已就緒(章程、規格、計劃和任務)
- 解析 `tasks.md` 中的任務分解
- 按正確順序執行任務, 尊重依賴關係和並行執行標記
- 遵循任務計劃中定義的 TDD 方法
- 提供進度更新並適當處理錯誤

>[!IMPORTANT]
>AI代理將執行本地CLI命令(如 `dotnet`、`npm` 等)- 確保你在機器上安裝了所需的工具.

實施完成後, 測試應用程式並解決任何在CLI日誌中可能不可見的執行時錯誤(例如, 瀏覽器控制檯錯誤). 你可以將此類錯誤複製貼上回AI代理以進行解決.

</details>

---

## 🔍 故障排除

### Linux上的Git憑據管理器

如果你在Linux上遇到Git身份驗證問題, 可以安裝Git憑據管理器: 

```bash
#!/usr/bin/env bash
set -e
echo "正在下載Git憑據管理器v2.6.1..."
wget https://github.com/git-ecosystem/git-credential-manager/releases/download/v2.6.1/gcm-linux_amd64.2.6.1.deb
echo "正在安裝Git憑據管理器..."
sudo dpkg -i gcm-linux_amd64.2.6.1.deb
echo "正在配置Git使用GCM..."
git config --global credential.helper manager
echo "正在清理..."
rm gcm-linux_amd64.2.6.1.deb
```

## 👥 維護者

- Den Delimarsky ([@localden](https://github.com/localden))
- John Lam ([@jflam](https://github.com/jflam))

## 💬 支援

如需支援, 請開啟[GitHub issue](https://github.com/rackliu/spec-kit-tw/issues/new). 我們歡迎錯誤報告、功能請求和關於使用規格驅動開發的問題.

## 🙏 致謝

這個專案深受[John Lam](https://github.com/jflam)的工作和研究的影響並基於其成果.

## 📄 許可證

本專案根據MIT開源許可證的條款授權. 請參閱[LICENSE](./LICENSE)檔案瞭解完整條款.
