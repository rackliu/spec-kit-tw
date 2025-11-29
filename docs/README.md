# 文件

此資料夾包含Spec Kit的文件原始檔, 使用[DocFX](https://dotnet.github.io/docfx/)構建.

## 本地構建

要在本地構建文件: 

1. 安裝DocFX: 
   ```bash
   dotnet tool install -g docfx
   ```

2. 構建文件: 
   ```bash
   cd docs
   docfx docfx.json --serve
   ```

3. 在瀏覽器中開啟`http://localhost:8080`檢視文件.

## 結構

- `docfx.json` - DocFX配置檔案
- `index.md` - 主要文件主頁
- `toc.yml` - 目錄配置
- `installation.md` - 安裝指南
- `quickstart.md` - 快速開始指南
- `_site/` - 生成的文件輸出(git忽略)

## 部署

當更改推送到`main`分支時, 文件會自動構建並部署到GitHub Pages. 工作流程定義在`.github/workflows/docs.yml`中.
