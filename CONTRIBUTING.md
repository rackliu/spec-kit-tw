## 為 Spec Kit 做貢獻

你好! 我們很高興你願意為 Spec Kit 做出貢獻. 本專案的貢獻內容根據[專案開源許可證](LICENSE)向公眾釋出.

請注意, 本專案隨[貢獻者行為準則](CODE_OF_CONDUCT.md)一起釋出. 參與本專案即表示你同意遵守其條款.

## 執行和測試程式碼的先決條件

這些是在提交拉取請求(PR)過程中, 能夠在本地測試你的更改所需的一次性安裝.

1. 安裝 [Python 3.11+](https://www.python.org/downloads/)
1. 安裝 [uv](https://docs.astral.sh/uv/) 用於包管理
1. 安裝 [Git](https://git-scm.com/downloads)
1. 準備一個可用的 [AI 編碼代理](README.md#-supported-ai-agents)

<details>
<summary><b>💡 如果你使用 <code>VSCode</code> 或 <code>GitHub Codespaces</code> 作為 IDE 的提示</b></summary>

<br>

只要你的機器上安裝了 [Docker](https://docker.com)，你就可以透過這個 [VSCode 擴充套件](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) 利用 [Dev Containers](https://containers.dev)，輕鬆設定你的開發環境。由於專案根目錄中的 `.devcontainer/devcontainer.json` 檔案，上述工具已經預先安裝和配置。

為此，只需：

- 檢出倉庫
- 使用 VSCode 開啟
- 開啟 [命令面板](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette) 並選擇 "Dev Containers: Open Folder in Container..."

在 [GitHub Codespaces](https://github.com/features/codespaces) 上更簡單，因為它在開啟 codespace 時自動利用 `.devcontainer/devcontainer.json`。

</details>

## 提交拉取請求

>[!NOTE]
>如果你的拉取請求引入了對 CLI 或倉庫其他部分工作產生實質性影響的大型更改(例如, 引入新模板、引數或其他重大更改), 請確保該更改已**經過專案維護者的討論和同意**. 未經事先對話和同意的大型更改拉取請求將被關閉.

1. Fork 並克隆倉庫
1. 配置和安裝依賴項: `uv sync`
1. 確保 CLI 在你的機器上正常工作: `uv run specify-tw --help`
1. 建立新分支: `git checkout -b my-branch-name`
1. 進行更改, 新增測試, 並確保一切仍然正常工作
1. 如果相關, 使用範例專案測試 CLI 功能
1. 推送到你的 fork 並提交拉取請求
1. 等待你的拉取請求被審查和合並.

以下是一些可以增加你的拉取請求被接受機率的方法: 

- 遵循專案的編碼規格.
- 為新功能編寫測試.
- 如果你的更改影響使用者可見的功能, 請更新文件(`README.md`、`spec-driven.md`).
- 儘可能保持你的更改專注. 如果你想進行多個相互不依賴的更改, 考慮將它們作為單獨的拉取請求提交.
- 編寫[良好的提交訊息](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).
- 使用 Spec-Driven Development 工作流測試你的更改以確保相容性.

## 開發工作流

在處理 spec-kit 時:

1. 在你選擇的編碼代理中使用 `specify-tw` CLI 命令(`/speckit.specify`、`/speckit.plan`、`/speckit.tasks`)測試更改
2. 驗證 `templates/` 目錄中的模板是否正常工作
3. 測試 `scripts/` 目錄中的指令碼功能
4. 如果進行了重大的流程更改, 確保更新記憶體檔案(`memory/constitution.md`)

### 本地測試模板和命令更改

執行 `uv run specify-tw init` 會拉取已釋出的包，這些包不包括你的本地更改。
要在本地測試你的模板、命令和其他更改，請按照以下步驟操作：

1. **建立釋出包**

   執行以下命令生成本地包：
   ```
   ./.github/workflows/scripts/create-release-packages.sh v1.0.0
   ```

2. **將相關包複製到你的測試專案**

   ```
   cp -r .genreleases/sdd-copilot-package-sh/. <path-to-test-project>/
   ```

3. **開啟並測試代理**

   導航到你的測試專案資料夾並開啟代理來驗證你的實現。

## Spec Kit 中的 AI 貢獻

> [!IMPORTANT]
>
> 如果你使用**任何型別的 AI 輔助**為 Spec Kit 做出貢獻, 
> 必須在拉取請求或 issue 中披露.

我們歡迎並鼓勵使用 AI 工具來幫助改進 Spec Kit! 許多有價值的貢獻都透過 AI 輔助進行了程式碼生成、問題檢測和功能定義的增強.

也就是說, 如果你在為 Spec Kit 做貢獻時使用任何型別的 AI 輔助(例如, 代理、ChatGPT), 
**必須在拉取請求或 issue 中披露這一點**, 同時說明使用 AI 輔助的程度(例如, 文件註釋 vs 程式碼生成).

如果你的 PR 響應或評論是由 AI 生成的, 也要披露這一點.

作為例外, 瑣碎的間距或拼寫錯誤修復不需要披露, 只要更改僅限於程式碼的小部分或短語.

披露範例: 

> 此 PR 主要由 GitHub Copilot 編寫.

或者更詳細的披露: 

> 我諮詢了 ChatGPT 來理解程式碼庫, 但解決方案
> 完全由我手動編寫.

不披露這一點首先對拉取請求另一端的人類操作員是不禮貌的, 但也使得難以確定
對貢獻應用多少審查力度.

在一個完美的世界裡, AI 輔助會產生比任何人類同等或更高品質的工作. 那不是我們今天生活的世界, 在大多數情況下
在沒有人類監督或專業知識的迴圈中, 它生成無法合理維護或演進的程式碼.

### 我們在尋找什麼

提交 AI 輔助貢獻時, 請確保它們包括: 

- **明確披露 AI 使用** - 你對 AI 使用透明, 並說明你在貢獻中使用它的程度
- **人類理解和測試** - 你親自測試了更改並理解它們的作用
- **明確的理由** - 你可以解釋為什麼需要更改以及它如何適應 Spec Kit 的目標
- **具體證據** - 包括展示改進的測試用例、場景或範例
- **你自己的分析** - 分享你對端到端開發體驗的想法

### 我們會關閉的內容

我們保留關閉看起來是以下內容的貢獻的權利: 

- 未經驗證提交的未測試更改
- 不解決特定 Spec Kit 需求的通用建議
- 顯示沒有人類審查或理解的大批次提交

### 成功指南

關鍵是證明你理解並驗證了你提議的更改. 如果維護者可以輕易看出貢獻完全由 AI 生成而沒有人類輸入或測試, 它在提交前可能需要更多工作.

持續提交低品質 AI 生成更改的貢獻者可能會被維護者自行決定限制進一步貢獻.

請尊重維護者並披露 AI 輔助.

## 資源

- [Spec-Driven Development 方法論](./spec-driven.md)
- [如何為開源做貢獻](https://opensource.guide/how-to-contribute/)
- [使用拉取請求](https://help.github.com/articles/about-pull-requests/)
- [GitHub 幫助](https://help.github.com)
