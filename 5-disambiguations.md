# Disambiguations - Resolving Ambiguous Terminology

**Purpose:** Provide decision logic for OneStream terms that have multiple meanings depending on context.

**Critical:** OneStream has heavily overloaded terminology. Always disambiguate before retrieval.

---

## Master Disambiguation Index

Terms requiring disambiguation (15 critical cases):

1. View (4+ meanings)
2. Consolidation (3 meanings)
3. Profile (2 meanings)
4. Formula (2 meanings)
5. Rule (4+ meanings)
6. Unit (3 meanings)
7. Cell (2 meanings)
8. Member (2 meanings)
9. Dimension (2 meanings)
10. Calculate (2 meanings)
11. Entity (2 meanings)
12. Account (2 meanings)
13. Process (2 meanings)
14. Source (2 meanings)
15. Engine (2 meanings)

---

## Detailed Disambiguation Logic

### 1. "View" Ambiguity (MOST COMMON)

**Possible Meanings:**
- **Cube View** (presentation layer component) - 70% of cases
- **View** (IC Dimension member type) - 15% of cases
- **Input View** (property for data entry timing) - 10% of cases
- **SQL View** (Relational Blending feature) - 5% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "display", "report", "dashboard" | **Cube View** | High |
| "intercompany", "IC", "elimination" | **View** (IC member type) | High |
| "YTD", "Periodic", "data entry timing" | **Input View** property | High |
| "SQL", "query", "external", "Relational" | **SQL View** | High |
| "create", "build", "design" | **Cube View** (most common) | Medium |
| No specific signals | **Cube View** (default) | Medium |

**Decision Tree:**
```
Does query mention "intercompany" or "IC"?
  YES → View (IC member type)
  NO  → Does query mention "SQL" or "Relational Blending"?
          YES → SQL View
          NO  → Does query mention "YTD" or "Periodic"?
                  YES → Input View property
                  NO  → Cube View (default)
```

**Retrieval Actions:**
- If **Cube View**: Include Member Filters, Parameters, POV, Suppression
- If **View (IC)**: Include Consolidation Members, Elimination, Entity hierarchy
- If **Input View**: Include Workflow Profile, Data entry concepts
- If **SQL View**: Include Relational Blending, SQL configuration

---

### 2. "Consolidation" Ambiguity

**Possible Meanings:**
- **Consolidation Process** (calculation execution) - 60% of cases
- **Consolidation Members** (Top, Share, Elimination) - 30% of cases
- **Consolidation Dimension** (structural component) - 10% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "running", "executing", "performance", "timing" | **Consolidation Process** | High |
| "Top", "Share", "Elimination", "parent-child" | **Consolidation Members** | High |
| "dimension", "structure", "metadata" | **Consolidation Dimension** | High |
| "how does...work", "calculation" | **Consolidation Process** | Medium |
| No specific signals | **Consolidation Process** (default) | Medium |

**Decision Tree:**
```
Does query mention "Top", "Share", or "Elimination"?
  YES → Consolidation Members
  NO  → Does query mention "dimension" or "structure"?
          YES → Consolidation Dimension
          NO  → Consolidation Process (default)
```

**Retrieval Actions:**
- If **Process**: Include Data Units, Algorithm, Translation, Sequence
- If **Members**: Include Entity hierarchy, Ownership, IC rules
- If **Dimension**: Include Dimension structure basics, Member types

---

### 3. "Profile" Ambiguity

**Possible Meanings:**
- **Workflow Profile** (Data Unit scope definition) - 95% of cases
- **Time Profile** (calendar configuration) - 5% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "calendar", "periods", "fiscal year" | **Time Profile** | High |
| "data unit", "scenario", "workflow", "certification" | **Workflow Profile** | High |
| "create", "configure", "setup" | **Workflow Profile** (most likely) | Medium |
| No specific signals | **Workflow Profile** (default) | High |

**Decision Tree:**
```
Does query mention "calendar" or "periods"?
  YES → Time Profile
  NO  → Workflow Profile (default - 95% of cases)
```

**Retrieval Actions:**
- If **Workflow Profile**: Include Scenario Type, Parent/Child, Channels, Data Units
- If **Time Profile**: Include Time Dimension, Period configuration, Fiscal year

---

### 4. "Formula" Ambiguity

**Possible Meanings:**
- **Member Formula** (calculation attached to Member) - 70% of cases
- **Business Rule calculation** (VB.NET logic) - 30% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "member", "account", "simple", "one-line" | **Member Formula** | High |
| "complex", "VB.NET", "reusable", "Business Rule" | **Business Rule** | High |
| "attached to", "specific member" | **Member Formula** | Medium |
| "multiple members", "reuse" | **Business Rule** | Medium |
| No specific signals | **Member Formula** (try first) | Medium |

**Decision Tree:**
```
Does query mention "complex logic" or "VB.NET"?
  YES → Business Rule
  NO  → Does query mention "member" or "account"?
          YES → Member Formula
          NO  → Does query suggest reusability?
                  YES → Business Rule
                  NO  → Member Formula (default)
```

**Retrieval Actions:**
- If **Member Formula**: Include Dynamic vs Stored, BRApi syntax, Sequence
- If **Business Rule**: Include Types, Entry points, BRApi restrictions, Context

**Important:** Provide disambiguation note explaining when to use each.

---

### 5. "Rule" Ambiguity

**Possible Meanings:**
- **Business Rule** (calculation) - 50% of cases
- **Transformation Rule** (ETL logic) - 30% of cases
- **Confirmation Rule** (validation) - 15% of cases
- **Other rules** (security, workflow, etc.) - 5% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "calculation", "formula", "VB.NET" | **Business Rule** | High |
| "import", "load", "ETL", "transformation" | **Transformation Rule** | High |
| "validation", "confirmation", "approval" | **Confirmation Rule** | High |
| "calculation" without "import" | **Business Rule** | Medium |
| No specific signals | **Business Rule** (most common) | Medium |

**Decision Tree:**
```
Does query mention "import" or "ETL"?
  YES → Transformation Rule
  NO  → Does query mention "validation" or "confirmation"?
          YES → Confirmation Rule
          NO  → Business Rule (default)
```

**Retrieval Actions:**
- If **Business Rule**: Include Types, BRApi, Entry points, Calculation context
- If **Transformation Rule**: Include Data Management, Stage Engine, Mapping
- If **Confirmation Rule**: Include Workflow, Validation logic, Exceptions

---

### 6. "Unit" Ambiguity

**Possible Meanings:**
- **Data Unit** (calculation scope: Profile+Scenario+Time) - 80% of cases
- **Unit** (dimension member type) - 15% of cases
- **Organizational unit** (Entity concept) - 5% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "workflow", "scenario", "calculation scope" | **Data Unit** | High |
| "dimension", "member type" | **Unit member type** | High |
| "wrong value", "calculation", "consolidation" | **Data Unit** | High |
| No specific signals | **Data Unit** (default) | High |

**CRITICAL:** Data Unit (scope) ≠ Data Cell (value) - common confusion!

**Retrieval Actions:**
- If **Data Unit**: Include Workflow Profile, Scenario Type, Locking, Consolidation
- If **Unit member type**: Include Dimension Member properties

---

### 7. "Cell" Ambiguity

**Possible Meanings:**
- **Data Cell** (intersection value in Cube) - 90% of cases
- **Spreadsheet cell** (Excel Add-in context) - 10% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "value", "calculation", "intersection" | **Data Cell** | High |
| "Excel", "spreadsheet", "Add-in" | **Spreadsheet cell** | High |
| No specific signals | **Data Cell** (default) | High |

**CRITICAL:** Data Cell (value) ≠ Data Unit (scope) - explain difference!

---

### 8. "Member" Ambiguity

**Possible Meanings:**
- **Dimension Member** (metadata element) - 95% of cases
- **Security Group member** (user) - 5% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "account", "entity", "dimension", "hierarchy" | **Dimension Member** | High |
| "user", "security", "permission", "access" | **Security Group member** | High |
| No specific signals | **Dimension Member** (default) | High |

---

### 9. "Process" Ambiguity

**Possible Meanings:**
- **Consolidation Process** (calculation execution) - 60% of cases
- **Workflow Process** (approval/certification flow) - 40% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "calculation", "consolidation", "algorithm" | **Consolidation Process** | High |
| "approval", "workflow", "certification", "task" | **Workflow Process** | High |

---

### 10. "Engine" Ambiguity

**Possible Meanings:**
- **Finance Engine** (post-load calculation) - 50% of cases
- **Stage Engine** (pre-load validation) - 30% of cases
- **Consolidation engine** (calculation processor) - 20% of cases

**Context Signals:**

| Signal Words | Interpretation | Confidence |
|-------------|----------------|-----------|
| "after load", "calculation", "Business Rule" | **Finance Engine** | High |
| "validation", "before load", "import" | **Stage Engine** | High |
| "consolidation", "algorithm" | **Consolidation engine** | Medium |

---

## Warning Signals Table

**If you see these patterns, STOP and disambiguate:**

| Pattern | Ambiguity Risk | Action Required |
|---------|---------------|-----------------|
| Query contains only "View" | High (4 meanings) | Check for "report", "IC", "YTD", or "SQL" signals |
| Query contains only "Profile" | Medium (2 meanings) | Check for "calendar" vs. "workflow" signals |
| Query contains only "Rule" | High (4+ meanings) | Check for "calculation", "import", or "validation" signals |
| Query contains only "Consolidation" | Medium (3 meanings) | Check for "process", "members", or "dimension" signals |
| Query contains only "Unit" | Medium (3 meanings) | Check for "workflow" vs. "dimension" signals |
| "How do I..." with no noun | High | Need more context - ask clarifying question |
| "Can I..." with ambiguous terms | High | Disambiguate before answering feasibility |

---

## Disambiguation Algorithm

**Apply this sequence:**

1. **Scan query for warning signals** (see table above)
2. **If ambiguous term detected:**
   - Check for context signal words
   - Apply decision tree for that term
   - Select interpretation with highest confidence
3. **If confidence < Medium:**
   - Surface disambiguation note in results
   - Provide brief explanation of alternatives
   - Let user clarify intent
4. **Apply retrieval rules** for selected interpretation
5. **Validate** that exclusions for other meanings are applied

---

## Multi-Term Disambiguation

**When multiple ambiguous terms appear:**

**Example:** "How do I create a View for Consolidation?"

**Ambiguous terms detected:** "View" (4 meanings), "Consolidation" (3 meanings)

**Disambiguation process:**
1. Check "View" context → No signals → Default to Cube View
2. Check "Consolidation" context → "how...work" pattern → Default to Process
3. **However**: "View FOR Consolidation" suggests reporting consolidation results
4. **Final interpretation:** "Cube View displaying Consolidation results"

**Retrieval strategy:**
- Cube View documentation
- Consolidation Process (to understand what's being displayed)
- Member Filters (for selecting consolidation members)
- Parameters (for POV selection)

---

## Edge Cases & Special Handling

### Case 1: "Cube for reporting"
**Common confusion:** User likely means "Cube View" not "Cube"
**Action:** Retrieve Cube View + add disambiguation note

### Case 2: "Business Rule for Account"
**Common confusion:** User likely means "Member Formula"
**Action:** Retrieve Member Formula first + when to use Business Rule instead

### Case 3: "Workflow Channel for Entity"
**Common confusion:** User likely means "Workflow Profile assignment"
**Action:** Retrieve Workflow Profile + disambiguation

### Case 4: "Data Unit value"
**Critical confusion:** User likely means "Data Cell" not "Data Unit"
**Action:** Retrieve Data Cell + explain Data Unit vs Cell distinction

---

## Confidence Levels

**High Confidence (90%+):**
- Strong context signals present
- Unambiguous phrasing
- Technical terms used correctly

→ Apply interpretation, no disambiguation note needed

**Medium Confidence (60-89%):**
- Some context signals
- Could have alternate meaning
- Phrasing suggests most likely interpretation

→ Apply interpretation, add brief disambiguation note

**Low Confidence (<60%):**
- No clear context signals
- Multiple interpretations equally likely
- Vague phrasing

→ Provide top 2 interpretations, ask for clarification

---

## Integration with Retrieval

**Pre-retrieval:**
1. Scan for ambiguous terms (Master Index)
2. Apply disambiguation logic
3. Select interpretation
4. Expand query with disambiguated term

**Post-retrieval:**
1. Verify excluded meanings aren't in results
2. Add disambiguation note if confidence < High
3. Provide "See also" links for alternate meanings if helpful

---

**Disambiguation is critical for OneStream RAG accuracy. Always check before retrieval.**
