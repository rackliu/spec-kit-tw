# 安裝指南

## 前置要求

- **Linux/macOS**(或 Windows; 現在支援 PowerShell 指令碼, 無需 WSL)
- AI編碼助手: [Claude Code](https://www.anthropic.com/claude-code), [GitHub Copilot](https://code.visualstudio.com/), [Codebuddy CLI](https://www.codebuddy.ai/cli)或 [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [uv](https://docs.astral.sh/uv/) 用於包管理
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

## 安裝

### 初始化新專案

最簡單的入門方式是初始化一個新專案: 

```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <PROJECT_NAME>
```

或者在當前目錄中初始化: 

```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init .
# 或使用 --here 標誌
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init --here
```

### 指定 AI 助手

你可以在初始化時主動指定你的 AI 助手: 

```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --ai claude
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --ai gemini
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --ai copilot
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --ai codebuddy
```

### 指定指令碼型別(Shell vs PowerShell)

所有自動化指令碼現在同時提供 Bash(`.sh`)和 PowerShell(`.ps1`)兩種變體.

自動行為: 
- Windows 預設: `ps`
- 其他作業系統預設: `sh`
- 互動模式: 除非你傳遞 `--script` 引數, 否則會提示你選擇

強制指定特定指令碼型別: 
```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --script sh
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --script ps
```

### 忽略助手工具檢查

如果你希望獲取模板而不檢查正確的工具: 

```bash
uvx --from git+https://github.com/rackliu/spec-kit-tw.git specify-tw init <project_name> --ai claude --ignore-agent-tools
```

## 驗證

初始化後, 你應該在 AI 助手中看到以下可用命令: 
- `/speckit.specify` - 建立規格
- `/speckit.plan` - 生成實施計劃
- `/speckit.tasks` - 分解為可執行任務

`.specify/scripts` 目錄將同時包含 `.sh` 和 `.ps1` 指令碼.

## 故障排除

### Linux 上的 Git 憑據管理器

如果你在 Linux 上遇到 Git 身份驗證問題, 可以安裝 Git 憑據管理器: 

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
