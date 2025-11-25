---
description: 基於使用者需求為當前功能生成自定義檢查清單.
scripts:
  sh: scripts/bash/check-prerequisites.sh --json
  ps: scripts/powershell/check-prerequisites.ps1 -Json
---

## 清單目的: "需求編寫的單元測試"

**核心概念**: 清單是**需求編寫的單元測試** - 它們驗證特定領域中需求的品質、清晰度和完整性.

**不用於驗證/測試**: 
- ❌ 不是"驗證按鈕點選正確"
- ❌ 不是"測試錯誤處理有效"
- ❌ 不是"確認 API 返回 200"
- ❌ 不是檢查程式碼/實現是否符合規格

**用於需求品質驗證**: 
- ✅ "是否為所有卡片型別定義了視覺層次需求？"(完整性)
- ✅ "'突出顯示'是否透過具體尺寸/位置進行了量化？"(清晰度)
- ✅ "所有互動元素的懸停狀態需求是否一致？"(一致性)
- ✅ "是否為鍵盤導航定義了可訪問性需求？"(覆蓋度)
- ✅ "規格是否定義了 logo 影像載入失敗時的處理？"(邊緣情況)

**比喻**: 如果你的規格是用英文編寫的程式碼, 那麼清單就是它的單元測試套件. 你測試的是需求是否編寫良好、完整、明確並準備好實施 - 而不是實現是否有效.

## 使用者輸入

```text
$ARGUMENTS
```

在繼續之前, 你**必須**考慮使用者輸入(如果不為空).

## 執行步驟

1. **設定**: 從倉庫根目錄執行 `{SCRIPT}` 並解析JSON以獲取FEATURE_DIR和AVAILABLE_DOCS列表.
   - 所有檔案路徑必須是絕對路徑.
   - 對於引數中的單引號如"I'm Groot", 使用轉義語法: 例如 'I'\''m Groot'(或者儘可能使用雙引號: "I'm Groot").

2. **澄清意圖(動態)**: 推導最多三個初始上下文澄清問題(無預編目錄). 它們必須: 
   - 從使用者的表述 + 從規格/計劃/任務中提取的訊號生成
   - 只詢問實質上改變清單內容的資訊
   - 如果在`$ARGUMENTS`中已經明確, 則單獨跳過
   - 優先考慮精確性而非廣度

   Generation algorithm:
   1. Extract signals: feature domain keywords (e.g., auth, latency, UX, API), risk indicators ("critical", "must", "compliance"), stakeholder hints ("QA", "review", "security team"), and explicit deliverables ("a11y", "rollback", "contracts").
   2. Cluster signals into candidate focus areas (max 4) ranked by relevance.
   3. Identify probable audience & timing (author, reviewer, QA, release) if not explicit.
   4. Detect missing dimensions: scope breadth, depth/rigor, risk emphasis, exclusion boundaries, measurable acceptance criteria.
   5. Formulate questions chosen from these archetypes:
      - Scope refinement (e.g., "Should this include integration touchpoints with X and Y or stay limited to local module correctness?")
      - Risk prioritization (e.g., "Which of these potential risk areas should receive mandatory gating checks?")
      - Depth calibration (e.g., "Is this a lightweight pre-commit sanity list or a formal release gate?")
      - Audience framing (e.g., "Will this be used by the author only or peers during PR review?")
      - Boundary exclusion (e.g., "Should we explicitly exclude performance tuning items this round?")
      - Scenario class gap (e.g., "No recovery flows detected—are rollback / partial failure paths in scope?")

   Question formatting rules:
   - If presenting options, generate a compact table with columns: Option | Candidate | Why It Matters
   - Limit to A–E options maximum; omit table if a free-form answer is clearer
   - Never ask the user to restate what they already said
   - Avoid speculative categories (no hallucination). If uncertain, ask explicitly: "Confirm whether X belongs in scope."

   Defaults when interaction impossible:
   - Depth: Standard
   - Audience: Reviewer (PR) if code-related; Author otherwise
   - Focus: Top 2 relevance clusters

   Output the questions (label Q1/Q2/Q3). After answers: if ≥2 scenario classes (Alternate / Exception / Recovery / Non-Functional domain) remain unclear, you MAY ask up to TWO more targeted follow‑ups (Q4/Q5) with a one-line justification each (e.g., "Unresolved recovery path risk"). Do not exceed five total questions. Skip escalation if user explicitly declines more.

3. **理解使用者請求**: 結合 `$ARGUMENTS` + 澄清答案: 
   - 推導清單主題(例如: security, review, deploy, ux)
   - 整合使用者明確提到的必需專案
   - 將焦點選擇對映到類別框架
   - 從規格/計劃/任務中推斷任何缺失的上下文(不要虛構)

4. **載入功能上下文**: 從 FEATURE_DIR 讀取: 
   - spec.md: 功能需求和範圍
   - plan.md(如果存在): 技術細節、依賴關係
   - tasks.md(如果存在): 實施任務

   **上下文載入策略**: 
   - 僅載入與活動焦點區域相關的必要部分(避免全文轉儲)
   - 優先將長部分總結為簡潔的場景/需求要點
   - 使用漸進式披露: 僅在檢測到差距時新增後續檢索
   - 如果源文件很大, 生成臨時摘要專案而不是嵌入原始文字

5. **生成清單** - 建立"需求的單元測試": 
   - Create `FEATURE_DIR/checklists/` directory if it doesn't exist
   - Generate unique checklist filename:
     - Use short, descriptive name based on domain (e.g., `ux.md`, `api.md`, `security.md`)
     - Format: `[domain].md` 
     - If file exists, append to existing file
   - Number items sequentially starting from CHK001
   - Each `/speckit.checklist` run creates a NEW file (never overwrites existing checklists)

   **核心原則 - 測試需求, 而非實現**: 
   每個清單專案必須評估需求本身, 檢查: 
   - **完整性**: 所有必要的需求是否存在？
   - **清晰度**: 需求是否明確無歧義且具體？
   - **一致性**: 需求之間是否相互一致？
   - **可測量性**: 需求是否可以客觀驗證？
   - **覆蓋度**: 是否涵蓋了所有場景/邊緣情況？

   **類別結構** - 按需求品質維度分組專案: 
   - **需求完整性**(所有必要的需求是否已記錄？)
   - **需求清晰度**(需求是否具體且無歧義？)
   - **需求一致性**(需求是否一致且無衝突？)
   - **驗收標準品質**(成功標準是否可測量？)
   - **場景覆蓋度**(是否涵蓋了所有流程/情況？)
   - **邊緣情況覆蓋度**(是否定義了邊界條件？)
   - **非功能性需求**(效能、安全性、可訪問性等 - 是否已指定？)
   - **依賴關係和假設**(是否已記錄和驗證？)
   - **歧義和衝突**(什麼 NEEDS CLARIFICATION？)

   **如何編寫清單專案 - "需求編寫的單元測試"**: 
   
   ❌ **WRONG** (Testing implementation):
   - "Verify landing page displays 3 episode cards"
   - "Test hover states work on desktop"
   - "Confirm logo click navigates home"
   
   ✅ **CORRECT** (Testing requirements quality):
   - "Are the exact number and layout of featured episodes specified?" [Completeness]
   - "Is 'prominent display' quantified with specific sizing/positioning?" [Clarity]
   - "Are hover state requirements consistent across all interactive elements?" [Consistency]
   - "Are keyboard navigation requirements defined for all interactive UI?" [Coverage]
   - "Is the fallback behavior specified when logo image fails to load?" [Edge Cases]
   - "Are loading states defined for asynchronous episode data?" [Completeness]
   - "Does the spec define visual hierarchy for competing UI elements?" [Clarity]
   
   **專案結構**: 
   Each item should follow this pattern:
   - Question format asking about requirement quality
   - Focus on what's WRITTEN (or not written) in the spec/plan
   - Include quality dimension in brackets [Completeness/Clarity/Consistency/etc.]
   - Reference spec section `[Spec §X.Y]` when checking existing requirements
   - Use `[Gap]` marker when checking for missing requirements
   
   **按品質維度分類的範例**: 
   
   完整性: 
   - "Are error handling requirements defined for all API failure modes? [Gap]"
   - "Are accessibility requirements specified for all interactive elements? [Completeness]"
   - "Are mobile breakpoint requirements defined for responsive layouts? [Gap]"
   
   清晰度: 
   - "Is 'fast loading' quantified with specific timing thresholds? [Clarity, Spec §NFR-2]"
   - "Are 'related episodes' selection criteria explicitly defined? [Clarity, Spec §FR-5]"
   - "Is 'prominent' defined with measurable visual properties? [Ambiguity, Spec §FR-4]"
   
   一致性: 
   - "Do navigation requirements align across all pages? [Consistency, Spec §FR-10]"
   - "Are card component requirements consistent between landing and detail pages? [Consistency]"
   
   覆蓋度: 
   - "Are requirements defined for zero-state scenarios (no episodes)? [Coverage, Edge Case]"
   - "Are concurrent user interaction scenarios addressed? [Coverage, Gap]"
   - "Are requirements specified for partial data loading failures? [Coverage, Exception Flow]"
   
   可測量性: 
   - "Are visual hierarchy requirements measurable/testable? [Acceptance Criteria, Spec §FR-1]"
   - "Can 'balanced visual weight' be objectively verified? [Measurability, Spec §FR-2]"

   **場景分類與覆蓋度**(需求品質焦點): 
   - Check if requirements exist for: Primary, Alternate, Exception/Error, Recovery, Non-Functional scenarios
   - For each scenario class, ask: "Are [scenario type] requirements complete, clear, and consistent?"
   - If scenario class missing: "Are [scenario type] requirements intentionally excluded or missing? [Gap]"
   - Include resilience/rollback when state mutation occurs: "Are rollback requirements defined for migration failures? [Gap]"

   **可追溯性要求**: 
   - MINIMUM: ≥80% of items MUST include at least one traceability reference
   - Each item should reference: spec section `[Spec §X.Y]`, or use markers: `[Gap]`, `[Ambiguity]`, `[Conflict]`, `[Assumption]`
   - If no ID system exists: "Is a requirement & acceptance criteria ID scheme established? [Traceability]"

   **發現和解決問題**(需求品質問題): 
   Ask questions about the requirements themselves:
   - Ambiguities: "Is the term 'fast' quantified with specific metrics? [Ambiguity, Spec §NFR-1]"
   - Conflicts: "Do navigation requirements conflict between §FR-10 and §FR-10a? [Conflict]"
   - Assumptions: "Is the assumption of 'always available podcast API' validated? [Assumption]"
   - Dependencies: "Are external podcast API requirements documented? [Dependency, Gap]"
   - Missing definitions: "Is 'visual hierarchy' defined with measurable criteria? [Gap]"

   **內容整合**: 
   - Soft cap: If raw candidate items > 40, prioritize by risk/impact
   - Merge near-duplicates checking the same requirement aspect
   - If >5 low-impact edge cases, create one item: "Are edge cases X, Y, Z addressed in requirements? [Coverage]"

   **🚫 ABSOLUTELY PROHIBITED** - These make it an implementation test, not a requirements test:
   - ❌ Any item starting with "Verify", "Test", "Confirm", "Check" + implementation behavior
   - ❌ References to code execution, user actions, system behavior
   - ❌ "Displays correctly", "works properly", "functions as expected"
   - ❌ "Click", "navigate", "render", "load", "execute"
   - ❌ Test cases, test plans, QA procedures
   - ❌ Implementation details (frameworks, APIs, algorithms)
   
   **✅ REQUIRED PATTERNS** - These test requirements quality:
   - ✅ "Are [requirement type] defined/specified/documented for [scenario]?"
   - ✅ "Is [vague term] quantified/clarified with specific criteria?"
   - ✅ "Are requirements consistent between [section A] and [section B]?"
   - ✅ "Can [requirement] be objectively measured/verified?"
   - ✅ "Are [edge cases/scenarios] addressed in requirements?"
   - ✅ "Does the spec define [missing aspect]?"

6. **結構參考**: 按照 `templates/checklist-template.md` 中的規格模板生成清單, 包括標題、元部分、類別標題和 ID 格式. 如果模板不可用, 使用: H1 標題、purpose/created 元行、包含 `- [ ] CHK### <requirement item>` 行的 `##` 類別部分, ID 從 CHK001 開始全域性遞增.

7. **報告**: 輸出建立清單的完整路徑、專案數量, 並提醒使用者每次執行都會建立新檔案. 總結: 
   - 選擇的焦點區域
   - 深度級別
   - 執行者/時間
   - 任何整合的使用者明確指定的必需專案

**重要說明**: 每次 `/speckit.checklist` 命令呼叫都會建立一個使用簡短描述性名稱的清單檔案, 除非檔案已存在. 這允許: 

- 建立多種不同型別的清單(例如: `ux.md`, `test.md`, `security.md`)
- 使用簡單、易記的檔名來表明清單用途
- 在 `checklists/` 資料夾中輕鬆識別和導航

為避免混亂, 請使用描述性型別, 並在完成後清理過時的清單.

## 範例清單型別和範例專案

**UX 需求品質**: `ux.md`

範例專案(測試需求, 而非實現): 
- "Are visual hierarchy requirements defined with measurable criteria? [Clarity, Spec §FR-1]"
- "Is the number and positioning of UI elements explicitly specified? [Completeness, Spec §FR-1]"
- "Are interaction state requirements (hover, focus, active) consistently defined? [Consistency]"
- "Are accessibility requirements specified for all interactive elements? [Coverage, Gap]"
- "Is fallback behavior defined when images fail to load? [Edge Case, Gap]"
- "Can 'prominent display' be objectively measured? [Measurability, Spec §FR-4]"

**API 需求品質**: `api.md`

範例專案: 
- "Are error response formats specified for all failure scenarios? [Completeness]"
- "Are rate limiting requirements quantified with specific thresholds? [Clarity]"
- "Are authentication requirements consistent across all endpoints? [Consistency]"
- "Are retry/timeout requirements defined for external dependencies? [Coverage, Gap]"
- "Is versioning strategy documented in requirements? [Gap]"

**效能需求品質**: `performance.md`

範例專案: 
- "Are performance requirements quantified with specific metrics? [Clarity]"
- "Are performance targets defined for all critical user journeys? [Coverage]"
- "Are performance requirements under different load conditions specified? [Completeness]"
- "Can performance requirements be objectively measured? [Measurability]"
- "Are degradation requirements defined for high-load scenarios? [Edge Case, Gap]"

**安全需求品質**: `security.md`

範例專案: 
- "Are authentication requirements specified for all protected resources? [Coverage]"
- "Are data protection requirements defined for sensitive information? [Completeness]"
- "Is the threat model documented and requirements aligned to it? [Traceability]"
- "Are security requirements consistent with compliance obligations? [Consistency]"
- "Are security failure/breach response requirements defined? [Gap, Exception Flow]"

## 反例: 什麼不要做

**❌ 錯誤 - 這些測試實現, 而非需求: **

```markdown
- [ ] CHK001 - Verify landing page displays 3 episode cards [Spec §FR-001]
- [ ] CHK002 - Test hover states work correctly on desktop [Spec §FR-003]
- [ ] CHK003 - Confirm logo click navigates to home page [Spec §FR-010]
- [ ] CHK004 - Check that related episodes section shows 3-5 items [Spec §FR-005]
```

**✅ 正確 - 這些測試需求品質: **

```markdown
- [ ] CHK001 - Are the number and layout of featured episodes explicitly specified? [Completeness, Spec §FR-001]
- [ ] CHK002 - Are hover state requirements consistently defined for all interactive elements? [Consistency, Spec §FR-003]
- [ ] CHK003 - Are navigation requirements clear for all clickable brand elements? [Clarity, Spec §FR-010]
- [ ] CHK004 - Is the selection criteria for related episodes documented? [Gap, Spec §FR-005]
- [ ] CHK005 - Are loading state requirements defined for asynchronous episode data? [Gap]
- [ ] CHK006 - Can "visual hierarchy" requirements be objectively measured? [Measurability, Spec §FR-001]
```

**關鍵區別: **
- 錯誤: 測試系統是否正常工作
- 正確: 測試需求是否編寫正確
- 錯誤: 驗證行為
- 正確: 驗證需求品質
- 錯誤: "它是否做 X？"
- 正確: "X 是否明確指定？"
