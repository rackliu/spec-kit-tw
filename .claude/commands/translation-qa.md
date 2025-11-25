---
name: translation-qa
description: "自動化翻譯品質保證檢查和驗證"
---

使用者輸入: 
$ARGUMENTS

目標: 對翻譯結果進行全面的品質檢查, 確保翻譯品質達到釋出標準.

執行步驟: 

1. 完整性檢查
   - 檔案完整性: 確保所有需要翻譯的檔案都已處理
   - 內容完整性: 對比原版確保沒有遺漏內容
   - 格式完整性: 檢查Markdown格式、連結、圖片引用
   - 結構完整性: 驗證目錄結構、標題層級、列表格式

2. 翻譯品質檢查
   - 術語一致性: 對照術語表檢查術語使用
   - 語言品質: 檢查語法、表達、流暢度
   - 技術準確性: 驗證技術概念翻譯的準確性
   - 上下文一致性: 檢查相關檔案間的翻譯一致性

3. 功能驗證檢查
   - CLI命令: 驗證命令名稱和引數翻譯
   - 路徑引用: 確保路徑引用保持正確
   - 程式碼範例: 驗證程式碼塊保持原樣
   - 佔位符: 檢查佔位符格式和內容
   - **GitHub倉庫配置**: 驗證模板下載源為中文版倉庫
   - **包名一致性**: 確保包名使用 specify-tw
   - **命令統一性**: 檢查所有使用者可見命令使用 specify-tw

4. 自動化測試
   - 連結有效性測試
   - 格式渲染測試
   - CLI幫助文字測試
   - 模板檔案可用性測試

5. 品質評分和報告
   - 為每個檔案生成品質評分
   - 識別需要人工稽核的問題
   - 生成詳細的品質檢查報告
   - 提供修復建議和最佳化方案

行為規則:
- 參考 @TRANSLATION_STANDARDS.md 和 @TERMINOLOGY.md 進行多維評估
- 對關鍵檔案(如CLI相關)進行更嚴格檢查
- 識別並標記機器翻譯痕跡
- 檢查文化適應性和本地化品質
- 確保翻譯後的使用者體驗與原版一致
- 生成可操作的品質改進建議
- 建立品質基線, 便於後續版本對比

## 🔍 關鍵修復點專項檢查

### A. GitHub倉庫配置檢查 (必須透過)
```bash
# 檢查倉庫所有者
grep -n 'repo_owner = "rackliu"' src/specify_cli/__init__.py
# 期望結果: repo_owner = "rackliu"

# 檢查倉庫名稱
grep -n 'repo_name = "spec-kit-tw"' src/specify_cli/__init__.py
# 期望結果: repo_name = "spec-kit-tw"
```
**重要性**: 🔴 **嚴重** - 確保下載中文模板而非原版模板

### B. CLI命令統一性檢查 (必須透過)
```bash
# 檢查應用名稱
grep -n 'name="specify-tw"' src/specify_cli/__init__.py
# 期望結果: name="specify-tw"

# 檢查是否還有未修復的 specify 命令
grep -n "specify[^-]" src/specify_cli/__init__.py
# 期望結果: 無匹配項

# 檢查範例命令
grep -n "specify-tw init" src/specify_cli/__init__.py | wc -l
# 期望結果: 多個匹配項 (>5)
```
**重要性**: 🔴 **嚴重** - 確保使用者體驗一致性

### C. 使用者介面翻譯檢查 (必須透過)
```bash
# 檢查關鍵中文翻譯
grep -n "已準備就緒\|正在檢查\|提示：" src/specify_cli/__init__.py
# 期望結果: 找到對應的中文翻譯

# 檢查是否還有未翻譯的英文介面
grep -n -E "(Tip:|Checking for|ready to use|Display version)" src/specify_cli/__init__.py
# 期望結果: 無匹配項
```
**重要性**: 🟡 **重要** - 確保中文使用者體驗

### D. 包名一致性檢查 (必須透過)
```bash
# 檢查包名使用規格
grep -n "specify-tw-cli" src/specify_cli/__init__.py
# 期望結果: 只在文件字串中出現，不在程式碼邏輯中
```
**重要性**: 🟡 **重要** - 確保專案命名規格

### E. 技術變數保護檢查 (必須透過)
```bash
# 檢查技術變數名是否被錯誤翻譯
# ❌ 錯誤: 將 sys._specify_tracker_active 改為 sys._specify_cn_tracker_active
# ✅ 正確: 保持技術變數名為英文原樣
grep -n "_specify_tracker_active" src/specify_cli/__init__.py
# 期望結果: _specify_tracker_active (保持不變)

grep -n "scripts_root.*specify" src/specify_cli/__init__.py
# 期望結果: scripts_root = project_path / ".specify" / "scripts" (保持 .specify 不變)
```
**重要性**: 🔴 **嚴重** - 技術變數名不能翻譯，會影響功能

### F. 斜槓命令格式檢查 (必須透過)
```bash
# 檢查斜槓命令是否保持原版格式 (不新增 /speckit. 字首)
grep -n "/speckit\." src/specify_cli/__init__.py
# 期望結果: 無匹配項 (不應該有 /speckit. 字首)

# 檢查斜槓命令內容是否翻譯
grep -n -E "(建立專案原則|建立基線規格|建立實施計劃|生成可執行任務|執行實施)" src/specify_cli/__init__.py
# 期望結果: 找到對應的中文翻譯
```
**重要性**: 🟡 **重要** - 確保斜槓命令符合翻譯標準

## ⚠️ 同步保護機制

### 原版同步後的必檢項
1. **倉庫配置回滾**: 每次同步原版後必須重新設定 `repo_owner = "rackliu"`
2. **命令名稱保護**: 確保 `name="specify-tw"` 不被覆蓋
3. **翻譯保護**: 確保中文介面文字不被英文覆蓋
4. **功能驗證**: 同步後必須測試模板下載功能

### 🛠️ 快速驗證指令碼
```bash
#!/bin/bash
# quick-verify-fixes.sh - 快速驗證關鍵修復點
echo "🔍 驗證 Spec Kit TW 關鍵修復點..."

echo ""
echo "📍 A. GitHub倉庫配置檢查"
if grep -q 'repo_owner = "rackliu"' src/specify_cli/__init__.py; then
    echo "✅ 倉庫所有者正確 (rackliu)"
else
    echo "❌ 倉庫所有者需要修復"
fi

if grep -q 'repo_name = "spec-kit-tw"' src/specify_cli/__init__.py; then
    echo "✅ 倉庫名稱正確 (spec-kit-tw)"
else
    echo "❌ 倉庫名稱需要修復"
fi

echo ""
echo "📍 B. CLI命令統一性檢查"
if grep -q 'name="specify-tw"' src/specify_cli/__init__.py; then
    echo "✅ 應用名稱正確 (specify-tw)"
else
    echo "❌ 應用名稱需要修復"
fi

unfixed_specify=$(grep -c "specify[^-]" src/specify_cli/__init__.py || true)
if [ "$unfixed_specify" -eq 0 ]; then
    echo "✅ 命令名稱已統一 (無遺留 specify)"
else
    echo "❌ 發現 $unfixed_specify 處未修復的 specify 命令"
fi

specify_cn_count=$(grep -c "specify-tw init" src/specify_cli/__init__.py || true)
if [ "$specify_cn_count" -gt 5 ]; then
    echo "✅ 範例命令已更新 ($specify_cn_count 處)"
else
    echo "❌ 範例命令需要更新 (當前: $specify_cn_count 處)"
fi

echo ""
echo "📍 C. 使用者介面翻譯檢查"
if grep -q "已準備就緒" src/specify_cli/__init__.py; then
    echo "✅ 狀態資訊已翻譯"
else
    echo "❌ 狀態資訊需要翻譯"
fi

if grep -q "正在檢查" src/specify_cli/__init__.py; then
    echo "✅ 檢查資訊已翻譯"
else
    echo "❌ 檢查資訊需要翻譯"
fi

if grep -q "提示：" src/specify_cli/__init__.py; then
    echo "✅ 提示資訊已翻譯"
else
    echo "❌ 提示資訊需要翻譯"
fi

unfixed_english=$(grep -c -E "(Tip:|Checking for|ready to use|Display version)" src/specify_cli/__init__.py || true)
if [ "$unfixed_english" -eq 0 ]; then
    echo "✅ 英文介面文字已處理"
else
    echo "❌ 發現 $unfixed_english 處未翻譯的英文文字"
fi

echo ""
echo "📊 檢查彙總"
total_checks=10
passed_checks=$(
    grep -q 'repo_owner = "rackliu"' src/specify_cli/__init__.py && echo 1 ||
    grep -q 'repo_name = "spec-kit-tw"' src/specify_cli/__init__.py && echo 1 ||
    grep -q 'name="specify-tw"' src/specify_cli/__init__.py && echo 1 ||
    [ "$unfixed_specify" -eq 0 ] && echo 1 ||
    [ "$specify_cn_count" -gt 5 ] && echo 1 ||
    grep -q '已準備就緒' src/specify_cli/__init__.py && echo 1 ||
    grep -q '正在檢查' src/specify_cli/__init__.py && echo 1 ||
    grep -q '提示：' src/specify_cli/__init__.py && echo 1 ||
    [ "$unfixed_english" -eq 0 ] && echo 1 ||
    grep -q '_specify_tracker_active' src/specify_cli/__init__.py && echo 1 ||
    grep -q 'scripts_root.*specify' src/specify_cli/__init__.py && echo 1 ||
    grep -n "/speckit\." src/specify_cli/__init__.py | head -1 && echo 0 || echo 1
) | wc -l

echo "透過檢查: $passed_checks/$total_checks"
if [ "$passed_checks" -eq "$total_checks" ]; then
    echo "🎉 所有關鍵修復點驗證透過!"
    exit 0
else
    echo "⚠️  發現問題，需要修復"
    exit 1
fi
```

### 📝 檢查結果解讀
- **10/10 透過**: 所有關鍵修復點正確，可以進行釋出
- **8-9/10 透過**: 存在重要問題，必須修復
- **<8/10 透過**: 存在嚴重問題，不建議釋出
