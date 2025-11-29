# 升級指南

> 您已安裝 Spec Kit 並希望升級到最新版本以獲取新功能、錯誤修復或更新的斜槓命令。本指南涵蓋升級 CLI 工具和更新專案檔案。

---

## 快速參考

| 升級內容 | 命令 | 使用場景 |
|----------|-------|----------|
| **僅 CLI 工具** | `uv tool install specify-tw-cli --force --from git+https://github.com/rackliu/spec-kit-tw.git` | 獲取最新 CLI 功能而不影響專案檔案 |
| **專案檔案** | `specify-tw init --here --force --ai <your-agent>` | 更新專案中的斜槓命令、模板和指令碼 |
| **兩者** | 執行 CLI 升級，然後專案更新 | 推薦用於主要版本更新 |

---

## 第 1 部分：升級 CLI 工具

CLI 工具 (`specify-tw`) 與您的專案檔案是分開的。升級它以獲得最新功能和錯誤修復。

### 如果您使用 `uv tool install` 安裝

```bash
uv tool install specify-tw-cli --force --from git+https://github.com/rackliu/spec-kit-tw.git
```

### 如果您使用一次性 `uvx` 命令

無需升級——`uvx` 總是獲取最新版本。只需正常執行您的命令：

```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init --here --ai copilot
```

### 驗證升級

```bash
specify-tw check
```

這將顯示已安裝的工具並確認 CLI 正常工作。

---

## 第 2 部分：更新專案檔案

當 Spec Kit 釋出新功能（如新的斜槓命令或更新的模板）時，您需要重新整理專案的 Spec Kit 檔案。

### 什麼會更新？

執行 `specify-tw init --here --force` 將更新：

- ✅ **斜槓命令檔案** (`.claude/commands/`, `.github/prompts/`, 等)
- ✅ **指令碼檔案** (`.specify/scripts/`)
- ✅ **模板檔案** (`.specify/templates/`)
- ✅ **共享記憶體檔案** (`.specify/memory/`) - **⚠️ 請參閱下面的警告**

### 什麼是安全的？

這些檔案在升級過程中**永遠不會被觸碰**——模板包甚至不包含它們：

- ✅ **您的規格** (`specs/001-my-feature/spec.md`, 等) - **確認安全**
- ✅ **您的實施計劃** (`specs/001-my-feature/plan.md`, `tasks.md`, 等) - **確認安全**
- ✅ **您的原始碼** - **確認安全**
- ✅ **您的 git 歷史** - **確認安全**

`specs/` 目錄完全從模板包中排除，在升級過程中永遠不會被修改。

### 更新命令

在您的專案目錄中執行：

```bash
specify-tw init --here --force --ai <your-agent>
```

將 `<your-agent>` 替換為您的 AI 助手。請參閱 [支援的 AI 助手](../README.md#-supported-ai-agents) 列表

**範例：**

```bash
specify-tw init --here --force --ai copilot
```

### 理解 `--force` 標誌

沒有 `--force`，CLI 會警告您並要求確認：

```
警告：當前目錄不為空（25 項）
模板檔案將與現有內容合併，並可能覆蓋現有檔案
是否繼續？[y/N]
```

使用 `--force`，它會跳過確認並立即繼續。

**重要：您的 `specs/` 目錄始終是安全的。** `--force` 標誌隻影響模板檔案（命令、指令碼、模板、記憶體）。您在 `specs/` 中的功能規格、計劃和任務永遠不會包含在升級包中，也無法被覆蓋。

---

## ⚠️ 重要警告

### 1. 章程檔案將被覆蓋

**已知問題：** `specify-tw init --here --force` 目前會用預設模板覆蓋 `.specify/memory/constitution.md`，刪除您所做的任何自定義設定。

**解決方法：**

```bash
# 1. 在升級前備份您的章程
cp .specify/memory/constitution.md .specify/memory/constitution-backup.md

# 2. 執行升級
specify-tw init --here --force --ai copilot

# 3. 恢復您的自定義章程
mv .specify/memory/constitution-backup.md .specify/memory/constitution.md
```

或使用 git 來恢復它：

```bash
# 升級後，從 git 歷史恢復
git restore .specify/memory/constitution.md
```

### 2. 自定義模板修改

如果您自定義了 `.specify/templates/` 中的任何模板，升級將覆蓋它們。先備份它們：

```bash
# 備份自定義模板
cp -r .specify/templates .specify/templates-backup

# 升級後，手動合併回您的更改
```

### 3. 重複的斜槓命令（基於 IDE 的代理）

一些基於 IDE 的代理（如 Kilo Code、Windsurf）在升級後可能顯示**重複的斜槓命令**——舊版本和新版本都會出現。

**解決方案：** 手動從代理的資料夾中刪除舊的命令檔案。

**Kilo Code 範例：**

```bash
# 導航到代理的命令資料夾
cd .kilocode/rules/

# 列出檔案並識別重複項
ls -la

# 刪除舊版本（範例檔名 - 您的可能不同）
rm speckit.specify-old.md
rm speckit.plan-v1.md
```

重啟您的 IDE 以重新整理命令列表。

---

## 常見場景

### 場景 1："我只想要新的斜槓命令"

```bash
# 升級 CLI（如果使用持久安裝）
uv tool install specify-tw-cli --force --from git+https://github.com/rackliu/spec-kit-tw.git

# 更新專案檔案以獲取新命令
specify-tw init --here --force --ai copilot

# 如果自定義了章程，則恢復
git restore .specify/memory/constitution.md
```

### 場景 2："我自定義了模板和章程"

```bash
# 1. 備份自定義內容
cp .specify/memory/constitution.md /tmp/constitution-backup.md
cp -r .specify/templates /tmp/templates-backup

# 2. 升級 CLI
uv tool install specify-tw-cli --force --from git+https://github.com/rackliu/spec-kit-tw.git

# 3. 更新專案
specify-tw init --here --force --ai copilot

# 4. 恢復自定義內容
mv /tmp/constitution-backup.md .specify/memory/constitution.md
# 如需要，手動合併模板更改
```

### 場景 3："我在 IDE 中看到重複的斜槓命令"

這發生在基於 IDE 的代理中（Kilo Code、Windsurf、Roo Code 等）。

```bash
# 查詢代理資料夾（範例：.kilocode/rules/）
cd .kilocode/rules/

# 列出所有檔案
ls -la

# 刪除舊命令檔案
rm speckit.old-command-name.md

# 重啟您的 IDE
```

### 場景 4："我在沒有 Git 的專案中工作"

如果您使用 `--no-git` 初始化專案，仍然可以升級：

```bash
# 手動備份您自定義的檔案
cp .specify/memory/constitution.md /tmp/constitution-backup.md

# 執行升級
specify-tw init --here --force --ai copilot --no-git

# 恢復自定義內容
mv /tmp/constitution-backup.md .specify/memory/constitution.md
```

`--no-git` 標誌跳過 git 初始化，但不影響檔案更新。

---

## 使用 `--no-git` 標誌

`--no-git` 標誌告訴 Spec Kit **跳過 git 倉庫初始化**。這在以下情況下有用：

- 您以不同方式管理版本控制（Mercurial、SVN 等）
- 您的專案是具有現有 git 設定的更大 monorepo 的一部分
- 您在實驗中，還不想使用版本控制

**在初始設定期間：**

```bash
specify-tw init my-project --ai copilot --no-git
```

**在升級期間：**

```bash
specify-tw init --here --force --ai copilot --no-git
```

### `--no-git` 不做什麼

❌ 不阻止檔案更新
❌ 不跳過斜槓命令安裝
❌ 不影響模板合併

它**只**跳過執行 `git init` 和建立初始提交。

### 沒有 Git 的工作

如果您使用 `--no-git`，您需要手動管理功能目錄：

**在使用規劃命令之前設定 `SPECIFY_FEATURE` 環境變數：**

```bash
# Bash/Zsh
export SPECIFY_FEATURE="001-my-feature"

# PowerShell
$env:SPECIFY_FEATURE = "001-my-feature"
```

這告訴 Spec Kit 在建立規格、計劃和任務時要使用哪個功能目錄。

**為什麼這很重要：** 沒有 git，Spec Kit 無法檢測您當前的分支名來確定活動功能。環境變數手動提供該上下文。

---

## 故障排除

### "升級後斜槓命令不顯示"

**原因：** 代理沒有重新載入命令檔案。

**修復：**

1. **完全重啟您的 IDE/編輯器**（不只是重新載入視窗）
2. **對於基於 CLI 的代理**，驗證檔案存在：
   ```bash
   ls -la .claude/commands/      # Claude Code
   ls -la .gemini/commands/       # Gemini
   ls -la .cursor/commands/       # Cursor
   ```
3. **檢查代理特定設定：**
   - Codex 需要 `CODEX_HOME` 環境變數
   - 一些代理需要工作區重啟或快取清除

### "我丟失了章程的自定義內容"

**修復：** 從 git 或備份恢復：

```bash
# 如果您在升級前提交了
git restore .specify/memory/constitution.md

# 如果您手動備份了
cp /tmp/constitution-backup.md .specify/memory/constitution.md
```

**預防：** 在升級前始終提交或備份 `constitution.md`。

### "警告：當前目錄不為空"

**完整警告訊息：**
```
警告：當前目錄不為空（25 項）
模板檔案將與現有內容合併，並可能覆蓋現有檔案
是否繼續？[y/N]
```

**這意味著什麼：**

當您在已有檔案的目錄中執行 `specify-tw init --here`（或 `specify-tw init .`）時會出現此警告。它告訴您：

1. **目錄有現有內容** - 在範例中，25 個檔案/資料夾
2. **檔案將合併** - 新模板檔案將新增到現有檔案旁邊
3. **一些檔案可能被覆蓋** - 如果您已有 Spec Kit 檔案（`.claude/`、`.specify/` 等），它們將被新版本替換

**什麼會被覆蓋：**

只有 Spec Kit 基礎設施檔案：
- 代理命令檔案（`.claude/commands/`、`.github/prompts/` 等）
- `.specify/scripts/` 中的指令碼
- `.specify/templates/` 中的模板
- `.specify/memory/` 中的記憶體檔案（包括章程）

**什麼不會被觸動：**

- 您的 `specs/` 目錄（規格、計劃、任務）
- 您的原始碼檔案
- 您的 `.git/` 目錄和 git 歷史
- 任何不屬於 Spec Kit 模板的其他檔案

**如何響應：**

- **輸入 `y` 並按 Enter** - 繼續合併（推薦升級時）
- **輸入 `n` 並按 Enter** - 取消操作
- **使用 `--force` 標誌** - 完全跳過此確認：
  ```bash
  specify-tw init --here --force --ai copilot
  ```

**當您看到此警告時：**

- ✅ **預期** 在升級現有 Spec Kit 專案時
- ✅ **預期** 在將 Spec Kit 新增到現有程式碼庫時
- ⚠️ **意外** 如果您認為您在空目錄中建立新專案

**預防提示：** 在升級前，如果您自定義了 `.specify/memory/constitution.md`，請提交或備份它。

### "CLI 升級似乎不工作"

驗證安裝：

```bash
# 檢查已安裝的工具
uv tool list

# 應該顯示 specify-tw-cli

# 驗證路徑
which specify-tw

# 應該指向 uv 工具安裝目錄
```

如果未找到，重新安裝：

```bash
uv tool uninstall specify-tw-cli
uv tool install specify-tw-cli --from git+https://github.com/rackliu/spec-kit-tw.git
```

### "我每次開啟專案都需要執行 specify 嗎？"

**簡短回答：** 不，您只需要每個專案執行一次 `specify-tw init`（或升級時）。

**解釋：**

`specify-tw` CLI 工具用於：
- **初始設定：** `specify-tw init` 在您的專案中引導 Spec Kit
- **升級：** `specify-tw init --here --force` 更新模板和命令
- **診斷：** `specify-tw check` 驗證工具安裝

一旦您運行了 `specify-tw init`，斜槓命令（如 `/speckit.specify`、`/speckit.plan` 等）就**永久安裝**在您專案的代理資料夾中（`.claude/`、`.github/prompts/` 等）。您的 AI 助手直接讀取這些命令檔案——無需再次執行 `specify-tw`。

**如果您的代理無法識別斜槓命令：**

1. **驗證命令檔案存在：**
   ```bash
   # 對於 GitHub Copilot
   ls -la .github/prompts/

   # 對於 Claude
   ls -la .claude/commands/
   ```

2. **完全重啟您的 IDE/編輯器**（不只是重新載入視窗）

3. **檢查您在正確的目錄**中運行了 `specify-tw init`

4. **對於某些代理**，您可能需要重新載入工作區或清除快取

**相關問題：** 如果 Copilot 無法開啟本地檔案或意外使用 PowerShell 命令，這通常是 IDE 上下文問題，與 `specify-tw` 無關。請嘗試：
- 重啟 VS Code
- 檢查檔案許可權
- 確保工作區資料夾正確開啟

---

## 版本相容性

Spec Kit 在主要版本中遵循語義版本控制。CLI 和專案檔案設計為在同一主要版本內相容。

**最佳實踐：** 透過在主要版本更改時一起升級兩者來保持 CLI 和專案檔案同步。

---

## 後續步驟

升級後：

- **測試新的斜槓命令：** 執行 `/speckit.constitution` 或其他命令以驗證一切正常
- **檢視釋出說明：** 檢查 [GitHub Releases](https://github.com/rackliu/spec-kit-tw/releases) 獲取新功能和重大更改
- **更新工作流：** 如果添加了新命令，更新您團隊的開發工作流
- **檢查文件：** 訪問 [github.io/spec-kit](https://github.github.io/spec-kit/) 獲取更新的指南
