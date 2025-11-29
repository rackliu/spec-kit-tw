---
name: translation-review
description: "Review and fix translation quality between spec-kit original and Chinese localized version"
---

使用者輸入可以直接由代理提供或作為命令引數提供給你 - 你**必須**考慮它(如果不為空).

使用者輸入: 

$ARGUMENTS

目標: 系統性地review原專案spec-kit與中文版之間的翻譯品質, 識別並修復所有翻譯錯誤、術語不一致和功能邏輯問題.

執行步驟: 

1. 驗證環境準備, 使用tree命令來檢查這些項, 需要完全同步的使用rsync命令確保同步
   - 確認spec-kit目錄存在且包含原版檔案
   - 確認templates目錄結構和spec-kit/templates保持一致
   - 確認memory目錄結構和spec-kit/docs保持一致
   - 確認docs目錄結構和spec-kit/docs保持一致
   - 確認src目錄結構和spec-kit/src保持一致
   - 確認scripts目錄結構和spec-kit/scripts保持一致(需完全同步)
   - 確認.devcontainer目錄結構和spec-kit/.devcontainer保持一致(需完全同步)
   - 確認media目錄結構和spec-kit/media保持一致(需完全同步)
   - 確認AGENTS.md檔案存在且與spec-kit/AGENTS.md一致(需完全同步)
   - 確認pyproject.toml配置檔案與原版結構一致
   
2. review核心md檔案翻譯品質
  - 深度遍歷 templates, memory, docs 三個目錄, 對找到的每個md檔案, 對比原版對應檔案, review翻譯品質. 此步驟使用Task工具並行執行

3. review專案級別md檔案翻譯品質, 以下子項務必使用Task工具並行處理
  - review spec-driven.md (對比原版 spec-kit/spec-driven.md) 的翻譯品質
  - review SUPPORT.md (對比原版 spec-kit/SUPPORT.md) 的翻譯品質
  - review SECURITY.md (對比原版 spec-kit/SECURITY.md) 的翻譯品質
  - review README.md (對比原版 spec-kit/README.md) 的翻譯品質
  - review CONTRIBUTING.md (對比原版 spec-kit/CONTRIBUTING.md) 的翻譯品質
  - review CODE_OF_CONDUCT.md (對比原版 spec-kit/CODE_OF_CONDUCT.md) 的翻譯品質
  
4. review src/specify_cli 目錄下python檔案的功能與翻譯品質
   - 遍歷 src/specify_cli 下的python檔案, 對比原版檔案, review其功能是否保持一致, 是否對指令碼中的文案進行了適當的翻譯

5. 檢查.github/目錄更新情況
   - 對比原版.github/目錄結構, 列出新增或修改的檔案
   - 如有更新, 詳細說明變更內容並提供同步建議
   - 不強制要求同步, 僅提供資訊供使用者決策

6. 輸出結構化報告等待人類稽核: 
   - 報告應包含執行摘要、詳細問題列表、術語一致性檢查、功能驗證結果和修復建議
   - 參考 @TRANSLATION_STANDARDS.md 中的輸出報告結構要求

行為規則: 
- 必須對比原版spec-kit中的對應檔案
- 使用Task工具並行對比
- 所有檔案翻譯後, 必須確保和原版表達是一樣的語義, 不能新增或減少內容
- 確保修復後的功能與原版完全一致
- 翻譯標準參考 @TRANSLATION_STANDARDS.md, 術語表參考 @TERMINOLOGY.md
- 輸出詳細的修復報告, 按照錯誤分類進行優先順序排序
- 所有沒有問題, 請直接告訴使用者
