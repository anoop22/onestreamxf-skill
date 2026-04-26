# Quick Reference - Fast Lookup for Common Queries

**Purpose:** Handles 80% of OneStream queries with fast pattern matching and disambiguation.

**When to use:** Start here for every query before loading specialized modules.

---

## Source Posture

Use the best available evidence in this order:

1. Exact API/member reference, if the query names a method, class, property, or enum.
2. Official OneStream documentation for product behavior and configuration.
3. OneStream Developer Portal for Business Rule standards and extensibility guidance.
4. Additional OneStream reference documents available to the agent.
5. Public community or partner examples only as secondary implementation hints.

If the loaded reference documents do not answer the question, load `10-public-web-resources.md` and use official web search before answering.

---

## Pattern Recognition Table

Detect query type and apply appropriate expansion:

| If Query Contains | Pattern Type | Auto-Include Context |
|-------------------|--------------|---------------------|
| "How do I calculate" | Calculation | BRApi, Member Formula vs Business Rule, Consolidation sequence |
| "How do I load" | Data Import | Data Sources, Transformation Rules, Stage Engine |
| "How do I create report" | Presentation | Cube Views, Parameters, Member Filters, Dashboards |
| "How do I set up workflow" | Workflow | Workflow Profiles, Channels, Parent/Child, Locking |
| "Why is my consolidation" | Troubleshooting | Data Units, Algorithm, Translation, Prerequisites |
| "How do I configure security" | Security | Security Groups, Cube Access, Relationship Security |
| "What's the difference" | Comparison | BOTH concepts + use cases + disambiguation |
| "Can I use X with Y" | Integration | Layer boundaries, BRApi restrictions, Examples |
| "`args`, `api`, `globals`, `Main`, follow-up phrasing like `parameter variable` or `argument`, or code-shape terms like `class`, `function`, or `namespace` near a Business Rule signature" | Business Rule Signature / Object Model | Standard `Main` prototype, identifier role hierarchy, rule type, typed `*Args` / `*Api`, parameter variable vs type/class vs runtime argument |
| "How do I optimize" | Performance | Design patterns, Data Unit sizing, Best practices |
| "How do I extend" | Extensibility | Business Rules, BRApi, Extenders, External DLL |

---

## Code-Snippet / Programmatic Access Shortcut

**If query combines developer intent with a OneStream concept** (examples: `sample code`, `snippet`, `extract`, `programmatically`, `BRApi`, `DataTable`, `Dashboard DataSet`):

1. Treat it as an API/rule-context question, not a concept-only question.
2. Keep the user-facing concept intact (for example `Cube View`) but search likely exact identifiers first when the task implies execution.
3. For programmatic Cube View extraction, probe the `FdxExecuteCubeView` family before broad source search, then inspect adjacent variants such as time-pivot methods.
4. Retrieve signature, return type, required context objects, named payload arguments, and example-hosting rule types before drafting sample code.
5. If the question asks how to pass runtime parameters or dashboard prompts, inspect the signature field that actually carries the payload before broad concept search.
6. If the question is about returned values, rows, columns, or whether a dimension comes from filters vs POV, retrieve Cube View result-set behavior too: rows, columns, Member Filters, POV, suppression, and parameter overrides.
7. Compare the asked dimension against explicit method override arguments; if the dimension is not an explicit argument, inspect the Cube View definition and passed parameters before inferring behavior.
8. Pull companion identifiers used for rule context, parameter passing, or output-shape inspection when examples reference them (for example `DashboardDataSetArgs`, `NameValuePairs`, `NameValueFormatBuilder`, `FdxGetCubeViewOrDataUnitColumnList`, `FdxResultDataTable`).
9. Keep runtime parameter payloads separate from entity/scenario/time filter arguments unless the query explicitly asks about both.
10. Use concept docs as supporting context only; do not let generic presentation matches outrank exact API evidence.

---

## Business Rule Signature Token Shortcut

**If query mentions generic Business Rule signature tokens** (examples: `args`, `api`, `globals`, `Main`, `SessionInfo`, `BRGlobals`), asks whether one of them is a `class`, `function`, `namespace`, `parameter`, or `object`, **or is a short follow-up using generic programming vocabulary such as** `parameter variable`, `argument`, `passed value`, `type`, **or** `object reference` **after a Business Rule signature discussion**:

1. Treat it as a Business Rule invocation-context question, not a generic programming-vocabulary question.
2. If the current turn is a short follow-up to a Business Rule signature discussion, carry forward the last resolved signature token, rule type, and example prototype from conversational context before searching.
3. Retrieve the standard Business Rule `Main` prototype first to determine which parameters are stable vs rule-type-specific.
4. If the query asks `what is it?` or compares code constructs, resolve the identifier role hierarchy explicitly: namespace -> containing type/class -> `Main` function -> parameter variable.
5. Do not answer from bare `args` or `api` in isolation; pivot to the owning Business Rule type and its concrete `*Args` / `*Api` classes.
6. If the rule type is named, exact-match its companion classes first (for example `FinanceRulesArgs`, `FinanceRulesApi`, `DashboardDataSetArgs`).
7. If the rule type is not named, use the standard prototype plus one or two documented rule-type examples to establish the pattern before generalizing.
8. Map bare signature tokens or follow-up references back to the resolved prototype slot before describing them (for example `args` -> parameter variable typed as `FinanceRulesArgs` in a Finance rule).
9. If the question is really about programming terminology, keep the OneStream example anchored and distinguish the parameter variable name from its declared type/class and the runtime argument value/object reference.
10. Pull representative properties or sub-argument members only after confirming the owner `*Args` class and invocation context.
11. Keep `BRApi`, rule-type `api`, and `args` separate; do not collapse them into one generic "API" concept.
12. If helpful, confirm the pattern with one second rule-type example from a different context, but keep the owning rule type explicit.
13. If the user asks what `args` contains, retrieve entry-point indicators, payload properties, and child argument objects from the resolved `*Args` class.
14. Demote loose matches on generic terms such as `class`, `function`, `namespace`, `arg`, `argument`, `object`, or `parameter` unless they are attached to the documented Business Rule signature or resolved OneStream type.

---

## Cube View BR# / DataCell Runtime Shortcut

**If query mentions `GetDataCell("BR#[...]")`, `FinanceFunctionType.DataCell`, `DataCellArgs`, `FunctionName`, or `NameValuePairs` in a Cube View / Finance rule context:**

1. Treat it as a cross-layer runtime-payload question spanning Cube View caller syntax and Finance rule execution context.
2. Exact-match `FinanceFunctionType.DataCell`, `FinanceRulesArgs`, `DataCellArgs`, `FunctionName`, `NameValuePairs`, and `GetDataCell` before broad source search.
3. Retrieve both sides of the handoff together: Cube View `BR#[BRName=..., FunctionName=..., Name=Value]` syntax and the Finance rule branch that reads `args.DataCellArgs`.
4. Keep `args` -> `FinanceRulesArgs` -> `DataCellArgs` ownership explicit; do not describe `NameValuePairs` as a free-floating dictionary.
5. When the question is `where did this value come from?`, distinguish values inherited from the current Cube View cell intersection vs dimensions explicitly overridden in `api.Data.GetDataCell(...)`.
6. If the query is about output/rendering, retrieve `DataCell` return behavior before scalar `.CellAmount` patterns; do not assume the caller only needs a numeric amount.
7. Keep Cube View call syntax, Finance rule branching, and expression evaluation separate; do not collapse them into one generic `parameter passing` explanation.
8. Demote generic Cube View design/formatting results unless the query explicitly asks about layout.

---

## Exact API Identifier Shortcut

**If query contains an exact CamelCase API/member name** (example: `FdxExecuteCubeView`):

1. Search exact identifier hits in API docs first; do not start with broad source search.
2. Retrieve the containing class or namespace, signature, return type, named payload arguments, and nearby methods/properties with the same prefix/suffix.
3. Preserve embedded compound terms inside the identifier (for example `Cube View`) and pull that concept context too.
4. If the query is about passing runtime parameters, inspect the exact signature field that carries the payload before reading broad concept docs.
5. Pull surrounding runtime carrier/helper identifiers from the same usage cluster, especially `*Args`, `NameValuePairs`, builder/formatter types, and payload argument names such as `nvbParams`.
6. If the query is about returned values or output shape, retrieve Cube View rows, columns, Member Filters, POV, suppression, parameter overrides, and helper APIs such as `FdxGetCubeViewOrDataUnitColumnList` or `FdxResultDataTable`.
7. Keep runtime parameter payloads separate from entity/scenario/time POV filters; do not treat generic POV arguments as the answer to parameter-passing questions unless the query explicitly asks about them.
8. Answer usage questions from documented signature + owner context + adjacent API naming, then confirm with related concept docs.
9. Do not assert downstream usages unless they are explicitly documented.
10. Exclude generic matches created by splitting the identifier into loose tokens such as `cube`, `view`, or `execute` unless exact docs are exhausted.

## Fast Disambiguation Lookup

### "View" Ambiguity
| Context Signal | Interpretation |
|---------------|----------------|
| "display" or "report" | **Cube View** (presentation layer) |
| "intercompany" | **View** (IC Dimension member type) |
| "YTD" or "Periodic" | **Input View** (property) |
| "SQL" | **SQL View** (Relational Blending) |
| **Default** | **Cube View** |

### "Consolidation" Ambiguity
| Context Signal | Interpretation |
|---------------|----------------|
| "Top", "Share", "Elimination" | **Consolidation Members** |
| "running" or "executing" | **Consolidation Process** |
| "dimension" | **Consolidation Dimension** |
| **Default** | **Consolidation Process** |

### "Formula" Ambiguity
| Context Signal | Interpretation |
|---------------|----------------|
| "member" or "account" | **Member Formula** |
| "complex logic" | **Business Rule** |
| "Business Rule" | **Business Rule calculation** |
| **Default** | **Member Formula** (try first) |

### "Rule" Ambiguity
| Context Signal | Interpretation |
|---------------|----------------|
| "import" or "ETL" | **Transformation Rule** |
| "validation" | **Confirmation Rule** |
| "calculation" | **Business Rule** or Member Formula |
| "VB.NET" | **Business Rule** |
| **Default** | **Business Rule** |

### "Profile" Ambiguity
| Context Signal | Interpretation |
|---------------|----------------|
| "calendar" or "periods" | **Time Profile** |
| **Default** | **Workflow Profile** (99%) |

---

## Critical Inclusion Rules (Top 10)

**When retrieving [X], ALWAYS include [Y]:**

1. **Consolidation** → Data Units, Entity Hierarchy, Algorithm, Members
2. **Data Unit** → Workflow Profile, Scenario Type, Time, Locking
3. **Workflow Profile** → Scenario Type, Parent/Child, Channels
4. **Member Formula** → Dynamic vs Stored, BRApi syntax, Sequence position
5. **Cube View** → Member Filters, Parameters, POV, Suppression
6. **Business Rule** → Type, BRApi restrictions, Entry point, Context
7. **Translation** → FX Rates, Algorithm, Consolidation Members
8. **Data Management** → Data Sources, Transformation Rules, Stage Engine
9. **Extensible Dimensionality** → UD1-UD8, EntityDefault, Reporting implications
10. **Forms** → Form Templates, Form Child Profiles, Cube Views

---

## Critical Exclusion Rules (Top 10)

**When retrieving [X], EXCLUDE [Y] unless explicitly mentioned:**

1. **Cube View** → EXCLUDE Form details (different layer) unless "data entry" mentioned
2. **Member Formula** → EXCLUDE Business Rule details unless complexity suggests it
3. **Data Management** → EXCLUDE Finance Engine unless query spans both
4. **Workflow Profile** → EXCLUDE Workflow Channel unless "timing" mentioned
5. **BI-Blend** → EXCLUDE Relational Blending unless comparing
6. **Standard Cube** → EXCLUDE Hybrid/BI-Blend unless choosing design
7. **Dynamic Calculation** → EXCLUDE Consolidation sequence (doesn't participate)
8. **Stage Engine** → EXCLUDE Finance BRApi (not accessible)
9. **Extensible Document** → EXCLUDE Excel Add-in unless comparing
10. **Named Business Rule** → EXCLUDE Event Handler unless choosing type

---

## Prerequisite Chains by Role

### End Users
```
Dimension → Member → Cube → Cube View → Dashboard
```

### Data Entry Users
```
Dimension → Member → Cube → Workflow Profile → Form Template
```

### Administrators
```
Dimension → Cube → Data Source → Transformation Rule → Data Management
```

### Analysts
```
Dimension → Account → Member Formula → Consolidation → Translation
```

### Developers
```
Dimension → Cube → BRApi → Business Rule → Complex Expression
```

### Architects
```
Cube → Workflow Profile → Data Unit → Cube Reference → Consolidation
```

---

## Common Confusion Quick Fixes

| User Says | Likely Means | Retrieve |
|-----------|--------------|----------|
| "Create Cube for reporting" | Cube View | Cube View docs + **disambiguation note** |
| "Extract data from Cube View" | Programmatic API/rule context | `FdxExecuteCubeView` family + signature/return type + rule context objects + rows/columns/member filters vs POV |
| "Formula not saving" | Dynamic vs Stored | Storage property + calculation types |
| "Workflow Channel for Entity" | Workflow Profile | Profile assignment + disambiguation |
| "Business Rule for Account" | Member Formula | Member Formula first + when to use BR |
| "`args` / `api` / `Main` what is it?" | Signature token vs type/class confusion | Standard `Main` prototype + parameter variable vs typed `*Args` / `*Api` class + namespace only if asked |
| "`what is a function parameter variable?` or `is that an argument or parameter?` after discussing `args` / `api` / `Main`" | Follow-up programming-vocabulary question about a Business Rule signature | Re-anchor to last resolved signature token + standard `Main` prototype + parameter variable vs type/class vs runtime argument distinction |
| "Transform after load" | Business Rule | Business Rule + NOT Transformation Rule |
| "Extensible Account" | Not possible | UD1-UD8 only + **constraint explanation** |
| "BI-Blend for SQL" | Relational Blending | Relational Blending + disambiguation |
| "Data Unit wrong value" | Data Cell | Data Cell + Data Unit distinction |

---

## Performance Query Expansions

| Performance Context | Auto-Include |
|--------------------|--------------|
| "Large data volume" | Standard Large Sparse design, Data Unit sizing, BI-Blend option |
| "Slow consolidation" | Calculation sequence, Business Rule efficiency, Formula optimization |
| "Slow report" | Cube View optimization, Suppression, Member Filters, BI-Blend |
| "Sparse data" | BI-Blend, Suppression settings, Extensible Dimensionality |

---

## Layer-Based Retrieval

| If Query Mentions | Stay in Layer | Cross Layers Only If |
|-------------------|---------------|---------------------|
| Cube structure | Foundation | "Workflow" mentioned → Workflow Layer |
| Data entry | Data Collection | "Validation" → Workflow Layer |
| Calculation | Calculation | "Timing" → Workflow; "Display" → Presentation |
| Workflow | Workflow | "Calculation timing" → Calculation Layer |
| Reporting | Presentation | "Data entry" → Forms (Data Collection) |
| Security | Foundation | "Workflow access" → Workflow Layer |

---

## Context Signal Detection

### → Data Collection Layer
**Keywords:** "import", "load", "ETL", "source", "transformation", "validate"
**Retrieve:** Data Sources, Data Management, Stage Engine, Transformation Rules

### → Calculation Layer
**Keywords:** "formula", "calculate", "consolidate", "aggregate", "total", "translate"
**Retrieve:** Member Formulas, Business Rules, Consolidation, BRApi, Translation

### → Presentation Layer
**Keywords:** "report", "display", "dashboard", "view", "format", "chart"
**Retrieve:** Cube Views, Dashboards, Extensible Documents, Parameters

### → Workflow Layer
**Keywords:** "approval", "certification", "lock", "process", "task", "timing"
**Retrieve:** Workflow Profiles, Channels, Certification, Confirmation, Locking

### → Architecture/Design
**Keywords:** "design", "structure", "multiple cubes", "performance", "optimize"
**Retrieve:** Cube Design Patterns, Extensible Dimensionality, Best Practices

### → Security
**Keywords:** "permission", "access", "security", "role", "restrict", "group"
**Retrieve:** Security Groups, Cube Access, Relationship Security

---

## Quick Decision Trees

### "Should I use Member Formula or Business Rule?"

```
Is it attached to ONE specific Member?
  YES → Is logic simple (one-line formula)?
          YES → Member Formula
          NO  → Check if Business Rule is better
  NO  → Business Rule (reusable across members)

Is it called during consolidation automatically?
  YES → Member Formula OR Business Rule in Calculate function
  NO  → Business Rule (explicitly called)

Do I need to reuse this logic elsewhere?
  YES → Business Rule (can be called from multiple places)
  NO  → Member Formula (if member-specific)
```

### "Which Cube Design Pattern?"

```
Data characteristics:
  < 750k cells per Data Unit + mostly dense → Standard Cube
  > 750k cells per Data Unit + sparse → Standard Large Sparse
  Need fast consolidation + limited reporting → Hybrid Cube
  Need fast reporting + large sparse data → BI-Blend
  Need to query external SQL real-time → Relational Blending
```

### "Dynamic or Stored Calculation?"

```
Is performance during consolidation critical?
  YES → Dynamic (no consolidation impact)

Is report performance critical?
  YES → Stored (pre-calculated)

Is data queried frequently?
  YES → Stored
  NO  → Dynamic

Does calculation need to persist?
  YES → Stored
  NO  → Dynamic
```

---

## Top 20 Critical Relationships

```
1.  Cube contains 18 Dimensions
2.  Workflow Profile defines Data Unit scope
3.  Data Unit = Workflow Profile + Scenario + Time
4.  Cube View displays Cube data (read-only by default)
5.  Form allows data entry via Cube View
6.  Member Formula attached to Dimension Member
7.  Business Rule contains reusable logic
8.  Consolidation operates on Data Units
9.  Translation requires FX Rate table
10. Elimination requires IC Account setup
11. Workflow Profile has Parent/Child structure
12. Workflow Channel controls timing
13. Data Management uses Data Sources
14. Transformation Rules modify imported data
15. Stage Engine validates before load
16. Finance Engine calculates after load
17. Extensible Dimensionality only for Entity/UD1-UD8
18. BI-Blend aggregates existing Cube
19. Relational Blending queries external SQL
20. BRApi access depends on Business Rule Type
```

---

## Emergency Disambiguation Protocol

**When in doubt, follow this order:**

### 1. Check Architectural Layer Signals
- Foundation keywords → Structure/Security
- Data Collection keywords → Import/ETL
- Workflow keywords → Process/Approval
- Calculation keywords → Formulas/Consolidation
- Presentation keywords → Reports/Dashboards

### 2. Identify Implied User Role
- End User → Focus on Cube Views, Dashboards
- Data Entry → Focus on Forms, Workflow
- Administrator → Focus on Data Management, Security
- Analyst → Focus on Calculations, Consolidation
- Developer → Focus on Business Rules, BRApi
- Architect → Focus on Cube Design, Performance

### 3. Check for Prerequisite Gaps
- Advanced topic without basics → Include prerequisites
- Calculation question without Cube context → Add Cube basics
- Workflow question without Scenario → Add Scenario Type

### 4. Apply Default Interpretations
- "View" → **Cube View**
- "Profile" → **Workflow Profile**
- "Consolidation" → **Consolidation Process**
- "Rule" → **Business Rule**
- "Formula" → **Member Formula**

---

## Usage Workflow

### Pre-Processing (Before Semantic Search)
1. Detect pattern type (use Pattern Recognition Table)
2. Identify ambiguous terms (use Disambiguation Lookup)
3. Check for context signals (use Signal Detection)
4. Determine prerequisite gaps (use Prerequisite Chains)
5. Expand query appropriately

### Post-Processing (After Semantic Search)
1. Apply Inclusion Rules (add missing context)
2. Apply Exclusion Rules (remove irrelevant results)
3. Sort by priority (P1 concepts before P5 examples)
4. Add disambiguation notes if ambiguity detected

---

## When to Load Specialized Modules

**If still ambiguous after quick reference:**
→ Load `5-disambiguations.md` for detailed resolution logic

**If advanced topic detected:**
→ Load `4-prerequisites.md` for complete dependency chains

**If architectural question:**
→ Load `1-conceptual-architecture.md` + `3-architectural-layers.md`

**If complex retrieval logic needed:**
→ Load `9-retrieval-rules.md` for full rule engine

---

**This module handles 80% of queries. Only load additional modules when needed.**
