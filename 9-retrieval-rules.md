# Complete Retrieval Rules - Synthesis Engine

**Purpose:** Comprehensive rule engine synthesizing all domain intelligence for source-guided OneStream answers.

**This is the master ruleset.** Use after quick-reference for complex queries requiring full rule application.

## Public References

**Official first:**
- [Cube Views](https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html)
- [Cubes](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Cubes.html)
- [Data Units](https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Workflow%20Guides/Data%20Units.html)
- [Data Access / Slice Security](https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Cube/Data%20Access.html)
- [Business Rule Types](https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types)

**Supplemental public examples:**
- [OneStream Community: FdxExecuteCubeView parameters](https://community.onestreamsoftware.com/discussions/WorkflowDI/fdxexecutecubeview-parameters/13514)
- [OneStream Community: Parameter tag discussions](https://community.onestreamsoftware.com/tag/parameters)
- [MindStream Analytics: Cube View dashboard navigation](https://www.mindstreamanalytics.com/blog/onestream-cube-view-right-click-dashboard-navigation.html)

---

## Source Hierarchy

Apply retrieval rules to whatever OneStream reference documents and public sources the agent can access.

1. **Exact API/member reference:** use first for method, class, enum, property, and signature questions.
2. **Official OneStream documentation:** use first for product behavior, setup, security, workflow, Cube Views, dashboards, and design.
3. **OneStream Developer Portal:** use for Business Rule standards, extensibility patterns, logging, versioning, and developer conventions.
4. **Additional OneStream reference documents:** use when available, and cite where possible.
5. **Public community or partner examples:** use only as secondary implementation hints.

If only public web access is available, load `10-public-web-resources.md`, run official domain-restricted searches first, and cite the sources used.

---

## The 5-Tier Retrieval Priority System

```
P1: ESSENTIAL (Always include)
  -> Definitions, core concepts, direct answers

P2: CRITICAL CONTEXT (Include by default)
  -> Prerequisites, related concepts, architectural context

P3: SUPPORTING DETAILS (Include if relevant)
  -> Examples, best practices, common patterns

P4: ALTERNATIVE APPROACHES (Include if comparison needed)
  -> Other solutions, design patterns, trade-offs

P5: SUPPLEMENTARY (Include if space permits)
  -> Edge cases, advanced scenarios, detailed examples
```

---

## Master Inclusion Rules (20 Rules)

### R1: Consolidation → Complete Context
**When retrieving:** Consolidation (any variant)
**ALWAYS include:**
- Data Units (calculation scope)
- Entity Hierarchy (consolidation structure)
- Algorithm (calculation method)
- Consolidation Members (Top, Share, Elimination)
**Priority:** P1 (Process), P2 (Prerequisites)

---

### R2: Data Unit → Workflow Context
**When retrieving:** Data Unit
**ALWAYS include:**
- Workflow Profile (defines scope)
- Scenario Type (affects behavior)
- Time (period scope)
- Locking (state management)
**Priority:** P1 (Definition), P2 (Components)

---

### R3: Workflow Profile → Operational Context
**When retrieving:** Workflow Profile
**ALWAYS include:**
- Scenario Type (classification)
- Parent/Child relationships (hierarchy)
- Workflow Channels (timing)
**Priority:** P1 (Configuration), P2 (Relationships)

---

### R4: Member Formula → Calculation Context
**When retrieving:** Member Formula
**ALWAYS include:**
- Dynamic vs Stored property (execution model)
- BRApi syntax (formula language)
- Sequence position (execution order)
**Priority:** P1 (Definition), P2 (Properties)

---

### R5: Cube View → Presentation Context
**When retrieving:** Cube View
**ALWAYS include:**
- Member Filters (data selection)
- Parameters (variables)
- POV (Point of View)
- Suppression rules (row/column hiding)
**Priority:** P1 (Structure), P2 (Components)

**If query also shows developer intent** (`sample code`, `snippet`, `extract`, `programmatically`, `BRApi`, `DataTable`, `Dashboard DataSet`):
- Promote exact API lookup before broad source search
- Verify signature and return type from API docs before writing code
- Retrieve rule/context objects used by examples or calling patterns
- Pull adjacent extraction variants/sibling methods
- If the query asks how to pass runtime parameters or dashboard prompts, retrieve the exact signature plus the named payload argument and nearby helper identifiers (`*Args`, `NameValuePairs`, builder/formatter types) before broad source expansion
- If the query mentions `GetDataCell("BR#[...]")`, `FinanceFunctionType.DataCell`, `DataCellArgs`, `FunctionName`, or `NameValuePairs`, retrieve the full caller/runtime chain together: Cube View `BR#[BRName=..., FunctionName=..., Name=Value]` syntax, Finance rule `Main` prototype, `FinanceRulesArgs` -> `DataCellArgs`, and the exact `DataCell` branch
- Keep runtime parameter payloads separate from entity/scenario/time filter arguments unless the query explicitly asks about both
- Distinguish caller payload keys from POV/filter arguments and from dimensions explicitly overridden inside `api.Data.GetDataCell(...)`
- If the question is about what renders in the Cube View, prefer `DataCell` return behavior before scalar-only patterns
- If the real question is output shape (`what values`, `which accounts`, `returned columns`, `POV or filters`), retrieve the Cube View surfaces that govern the result set: rows, columns, Member Filters, POV, suppression, and parameter overrides
- Compare the asked dimension against explicit API override arguments before inferring whether it comes from method inputs, Cube View definition, or passed parameters
- Pull helper APIs such as `FdxGetCubeViewOrDataUnitColumnList` and `FdxResultDataTable` when the user is really asking about returned schema or dimensional context
- Do not invent a separate "POV-only" extract mode unless the API docs explicitly describe one
- Demote design-only Cube View tuning unless the query explicitly asks about layout or formatting
**Priority override:** P1 (Exact API + signature/result-shape evidence), P2 (Runtime context + override behavior), P3 (Cube View parameter behavior)

---

### R6: Business Rule → Programming Context
**When retrieving:** Business Rule
**ALWAYS include:**
- Business Rule Types (Calculate, Consolidate, etc.)
- BRApi restrictions (what's accessible)
- Entry point (where it's called from)
- Execution context (when it runs)

**If query includes generic signature tokens** (`args`, `api`, `globals`, `Main`, `SessionInfo`, `BRGlobals`) **or asks whether one of them is a** `class`, `function`, `namespace`, `parameter`, **or** `object`, **or is a short follow-up using generic programming vocabulary such as** `parameter variable`, `argument`, `passed value`, `type`, **or** `object reference` **after a Business Rule signature discussion**:
- Retrieve the standard Business Rule `Main` prototype first
- If the current turn is a short follow-up after a Business Rule signature discussion, carry forward the last resolved signature element and rule type from conversational context even if the new turn omits `args`, `api`, or `Main`
- Identify stable parameters vs rule-type-specific `*Api` / `*Args`
- Resolve the construct hierarchy explicitly: namespace -> containing type/class -> `Main` function -> parameter variable
- Anchor bare tokens to the resolved prototype slot before describing them (for example `args` is the parameter variable; `FinanceRulesArgs` is its type in a Finance rule)
- Distinguish the parameter variable name from its declared type/class and the runtime argument value/object reference when that is the actual question
- If the rule type is named, exact-match its companion classes before broad source search
- If the rule type is omitted, use one or two documented rule-type examples to establish the pattern and label them as examples
- Pull representative members from the resolved `*Args` class only after the owner type is confirmed
- Keep `BRApi`, rule-type `api`, and `args` distinct
- Demote generic language-level docs for `class`, `function`, `namespace`, `object`, or `parameter` unless they are tied to a resolved OneStream signature element

**If query mentions `FinanceFunctionType.DataCell`, `DataCellArgs`, `FunctionName`, `NameValuePairs`, or Cube View `BR#[...]` syntax:**
- Treat it as a Finance rule runtime-payload question, not a generic `args` explanation
- Retrieve the exact owner chain: `Main` -> `FinanceRulesArgs` -> `DataCellArgs` -> `FunctionName` / `NameValuePairs`
- Retrieve the matching Cube View caller syntax alongside the rule-side payload so parameter names can be traced end-to-end
- Keep Cube View caller syntax, Finance rule branch selection, and `api.Data.GetDataCell(...)` expression evaluation separate
- When the query asks where a value comes from, distinguish inherited current-cell intersection from explicitly overridden dimensions
- Do not assume `.CellAmount` is the desired return shape unless the docs or question ask for a scalar
**Priority:** P1 (Definition), P2 (Types and Access)

**Priority override:** P1 (prototype + construct-role mapping + owner classes + runtime payload types), P2 (caller syntax + DataCell handoff + context payload), P3 (illustrative rule-type examples)

---

### R7: Translation → FX Context
**When retrieving:** Translation
**ALWAYS include:**
- FX Rate table (rate source)
- Translation Algorithm (calculation method)
- Consolidation Members (which members translate)
**Priority:** P1 (Process), P2 (Requirements)

---

### R8: Data Management → ETL Context
**When retrieving:** Data Management
**ALWAYS include:**
- Data Sources (connections)
- Transformation Rules (data modification)
- Stage Engine (validation)
**Priority:** P1 (System), P2 (Components)

---

### R9: Extensible Dimensionality → UD Context
**When retrieving:** Extensible Dimensionality
**ALWAYS include:**
- UD1-UD8 (extensible dimensions)
- EntityDefault Members (default values)
- Reporting implications (query impact)
**Priority:** P1 (Feature), P2 (Prerequisites), P3 (Implications)

---

### R10: Forms → Data Entry Context
**When retrieving:** Forms
**ALWAYS include:**
- Form Templates (structure)
- Form Child Profiles (sub-forms)
- Cube Views (layout basis)
**Priority:** P1 (Structure), P2 (Components)

---

### R11: Performance Query → Design Context
**When retrieving:** Performance issues
**ALWAYS include:**
- Relevant design pattern (Standard, Large Sparse, BI-Blend)
- Data Unit sizing (scope impact)
- Best practices (optimization guidelines)
**Priority:** P1 (Diagnosis), P2 (Solutions)

---

### R12: Calculation Question → Sequence Context
**When retrieving:** Any calculation topic
**ALWAYS include:**
- Calculation sequence (execution order)
- Dynamic vs Stored distinction (if Member Formulas)
- Data Unit scope (calculation boundaries)
**Priority:** P2 (Context - helps understand behavior)

---

### R13: Security Question → Access Context
**When retrieving:** Security
**ALWAYS include:**
- Security Groups (user grouping)
- Cube Access (data permissions)
- Relationship Security (dimensional security)
**Priority:** P1 (Components), P2 (Mechanism)

---

### R14: Import Question → Stage/Finance Context
**When retrieving:** Data import/loading
**ALWAYS include:**
- Stage Engine (pre-load validation)
- Finance Engine (post-load calculation)
- Transformation Rules (data modification)
**Priority:** P1 (Process), P2 (Engines)

---

### R15: Workflow Question → Channel Context
**When retrieving:** Workflow timing
**ALWAYS include:**
- Workflow Channels (timing control)
- Parent/Child Profiles (hierarchy)
- Certification (approval flow)
**Priority:** P2 (Timing mechanism)

---

### R16: Dimension Question → Member Context
**When retrieving:** Dimension structure
**ALWAYS include:**
- Dimension Members (elements)
- Hierarchies (relationships)
- Member Properties (metadata)
**Priority:** P1 (Structure), P2 (Components)

---

### R17: Advanced Feature → Prerequisites
**When retrieving:** Any Tier 5 concept
**ALWAYS include:**
- Prerequisite concepts (Tier 0-2 basics)
- Learning path guidance (start here)
- "This is advanced" warning
**Priority:** P1 (Warning), P2 (Prerequisites)

---

### R18: Comparison Question → Both + Disambiguation
**When retrieving:** "Difference between X and Y"
**ALWAYS include:**
- X documentation
- Y documentation
- Disambiguation rules (when to use each)
- Use cases (practical guidance)
**Priority:** P1 (Both concepts), P2 (Disambiguation)

---

### R19: Integration Question → Boundary Rules
**When retrieving:** "Can I use X with Y"
**ALWAYS include:**
- Layer boundaries (architectural constraints)
- BRApi restrictions (if applicable)
- Examples (if feasible)
- Alternatives (if not feasible)
**Priority:** P1 (Answer), P2 (Explanation)

---

### R20: Troubleshooting → Multi-Layer Context
**When retrieving:** "Why isn't..."
**ALWAYS include:**
- All layers involved in data flow
- Common causes (prioritized)
- Validation steps
- Related configuration
**Priority:** P1 (Common causes), P2 (Validation)

---

## Master Exclusion Rules (15 Rules)

### E1: Cube View → Exclude Forms
**When retrieving:** Cube View
**EXCLUDE:** Form details (different layer)
**UNLESS:** "data entry" explicitly mentioned
**Reason:** Cube Views are read-only display; Forms are data entry

**For programmatic extraction / code requests:**
- Also EXCLUDE report-formatting-only guidance
- UNLESS the query asks how the Cube View definition affects returned columns, filters, or parameters
- Reason: the execution surface should outrank display-tuning guidance

---

### E2: Member Formula → Exclude Business Rule
**When retrieving:** Member Formula
**EXCLUDE:** Business Rule details
**UNLESS:** Query suggests complexity requiring Business Rule
**Reason:** Different calculation mechanisms; Member Formula is simpler

---

### E3: Data Management → Exclude Finance Engine
**When retrieving:** Data Management (import focus)
**EXCLUDE:** Finance Engine (post-load calculation)
**UNLESS:** Query spans both import and post-load
**Reason:** Different stages of data flow

---

### E4: Workflow Profile → Exclude Workflow Channel
**When retrieving:** Workflow Profile (configuration)
**EXCLUDE:** Workflow Channel details
**UNLESS:** "timing" or "when" mentioned
**Reason:** Channels are separate timing mechanism

---

### E5: BI-Blend → Exclude Relational Blending
**When retrieving:** BI-Blend (aggregation pattern)
**EXCLUDE:** Relational Blending (SQL pass-through)
**UNLESS:** Comparing design patterns
**Reason:** Different features with similar names

---

### E6: Standard Cube → Exclude Alternative Designs
**When retrieving:** Standard Cube
**EXCLUDE:** Hybrid, BI-Blend, Large Sparse details
**UNLESS:** "choosing design" or "comparison" mentioned
**Reason:** Avoid confusion with alternative patterns

---

### E7: Dynamic Calculation → Exclude Consolidation Sequence
**When retrieving:** Dynamic Member Formula
**EXCLUDE:** Consolidation sequence details
**REASON:** Dynamic calcs don't participate in consolidation
**INCLUDE:** Explanation of why (P2 context)

---

### E8: Stage Engine → Exclude Finance BRApi
**When retrieving:** Stage Engine (pre-load)
**EXCLUDE:** BRApi details (only in Finance Engine)
**REASON:** Architectural boundary - BRApi not accessible from Stage
**INCLUDE:** Alternative approaches (Transformation Rules)

---

### E9: Extensible Document → Exclude Excel Add-in
**When retrieving:** Extensible Document
**EXCLUDE:** Excel Add-in details
**UNLESS:** Comparing document approaches
**REASON:** Different technologies

---

### E10: Named Business Rule → Exclude Event Handler
**When retrieving:** Named Business Rule
**EXCLUDE:** Event Handler details
**UNLESS:** "choosing type" mentioned
**REASON:** Different Business Rule types with different use cases

---

### E11: Cube (Storage) → Exclude Cube View (Presentation)
**When retrieving:** Cube structure/design
**EXCLUDE:** Cube View presentation details
**UNLESS:** Query spans both layers
**REASON:** Different architectural layers; #1 confusion source

---

### E12: Transformation Rule → Exclude Business Rule
**When retrieving:** Transformation Rule (ETL)
**EXCLUDE:** Business Rule (calculation)
**REASON:** Different purposes; both called "Rules" but not interchangeable

---

### E13: Confirmation Rule → Exclude Business Rule
**When retrieving:** Confirmation Rule (validation)
**EXCLUDE:** Business Rule (calculation)
**REASON:** Different rule types; terminology overlap

---

### E14: Time Profile → Exclude Workflow Profile
**When retrieving:** Time Profile (calendar)
**EXCLUDE:** Workflow Profile (Data Unit scope)
**REASON:** Different "Profile" types; rare confusion but critical

---

### E15: Data Cell → Exclude Data Unit
**When retrieving:** Data Cell (value)
**EXCLUDE:** Data Unit (scope) unless explaining difference
**INCLUDE:** Distinction explanation (P2 - critical to understand)
**REASON:** Common confusion; completely different concepts

---

## Master Disambiguation Rules (20 Rules)

### D1: "View" Detection
**Ambiguous term:** "View"
**Check for signals:**
- "display", "report" → Cube View
- "intercompany", "IC" → View (member type)
- "YTD", "Periodic" → Input View property
- "SQL" → SQL View
**Default:** Cube View
**Confidence threshold:** High (90%+) required for no disambiguation note

---

### D2: "Consolidation" Detection
**Ambiguous term:** "Consolidation"
**Check for signals:**
- "running", "executing" → Consolidation Process
- "Top", "Share", "Elimination" → Consolidation Members
- "dimension" → Consolidation Dimension
**Default:** Consolidation Process
**Always disambiguate:** Include brief note on other meanings

---

### D3: "Profile" Detection
**Ambiguous term:** "Profile"
**Check for signals:**
- "calendar", "periods" → Time Profile
- Everything else → Workflow Profile
**Default:** Workflow Profile (99%)
**Disambiguation note:** Only if "calendar" mentioned

---

### D4: "Formula" Detection
**Ambiguous term:** "Formula"
**Check for signals:**
- "member", "account", "simple" → Member Formula
- "complex", "VB.NET", "reusable" → Business Rule
**Default:** Member Formula
**Include:** Decision tree for "when to use Business Rule instead"

---

### D5: "Rule" Detection
**Ambiguous term:** "Rule"
**Check for signals:**
- "calculation", "VB.NET" → Business Rule
- "import", "ETL" → Transformation Rule
- "validation" → Confirmation Rule
**Default:** Business Rule
**Disambiguation note:** Always (4+ meanings)

---

### D6: Layer Signal Detection
**Check query for layer keywords:**
- Foundation: "architecture", "structure", "security"
- Metadata: "dimension", "member", "hierarchy"
- Data Collection: "import", "load", "form"
- Workflow: "approval", "certification", "lock"
- Calculation: "calculate", "consolidate", "formula"
- Business Rules: "VB.NET", "code", "BRApi"
- Presentation: "report", "display", "dashboard"
**Action:** Focus retrieval on detected layer(s)
**Override:** If Presentation signals co-occur with developer intent (`sample code`, `snippet`, `extract`, `programmatically`, `BRApi`, `DataTable`, `Dashboard DataSet`), tag both Presentation and Business Rules, then run exact identifier lookup before broad source search.
**Additional override:** If Business Rules signals co-occur with generic signature tokens (`args`, `api`, `globals`, `Main`, `SessionInfo`, `BRGlobals`), treat the query as a Business Rule signature/context question and resolve the owning `*Args` / `*Api` types before broad source search.
**Conversational follow-up override:** If the current turn is a short generic-programming follow-up (`what is a function parameter variable?`, `is that an argument or parameter?`, `what type is that?`) after a Business Rule signature discussion, inherit the last resolved signature token/rule type and treat it as a Business Rule signature/context question even if the new turn omits `args`, `api`, or `Main`.
**DataCell override:** If Presentation signals co-occur with `BR#[`, `GetDataCell`, `FinanceFunctionType.DataCell`, `DataCellArgs`, `FunctionName`, or `NameValuePairs`, tag both Presentation and Business Rules, then retrieve the Cube View caller syntax plus the Finance rule runtime payload before broad source search.
**Code-shape override:** If those tokens are paired with vocabulary such as `class`, `function`, `namespace`, `parameter`, `object`, or `what is this`, map the concrete signature element to its role in the prototype before retrieving generic programming explanations.

---

### D7: Role Signal Detection
**Infer user role from query:**
- End User: Focus on Cube Views, Dashboards
- Data Entry: Focus on Forms, Workflow
- Administrator: Focus on Data Management, Security
- Analyst: Focus on Calculations, Consolidation
- Developer: Focus on Business Rules, BRApi
- Architect: Focus on Cube Design, Performance
**Action:** Filter prerequisites and examples to role

---

### D8: Prerequisite Gap Detection
**Scan for Tier 5 concepts:**
- Extensible Dimensionality
- BI-Blend
- Relational Blending
- Standard Large Sparse
- Event Handlers
**Action:** Include Tier 0-2 prerequisites + warning

---

### D9: Compound Term Detection
**Scan for 45+ compound terms:**
- Cube View, Workflow Profile, Member Formula, etc.
**Also scan for exact API/member identifiers that embed those terms:**
- Example: `FdxExecuteCubeView` -> exact identifier + embedded `Cube View`
**Action:** Treat compounds as atomic, preserve embedded atomic terms inside identifiers, and apply exclusion rules to generic token matches.
**If the same query asks how to pass parameters or runtime values:** retrieve the exact signature plus the named payload argument and nearby helper identifiers (`*Args`, `NameValuePairs`, builder/formatter types) before broad source expansion, and do not let generic POV/filter matches substitute for that parameter-passing context unless explicitly requested.

---

### D10: Performance Context Detection
**Keywords:** "slow", "performance", "optimize", "large"
**Action:** Include design patterns + sizing + best practices

---

### D11: Troubleshooting Pattern Detection
**Keywords:** "why isn't", "not working", "error", "issue"
**Action:** Multi-layer retrieval + common causes prioritized

---

### D12: Comparison Request Detection
**Keywords:** "difference", "vs", "versus", "compare"
**Action:** Include both concepts + disambiguation + use cases

---

### D13: Feasibility Question Detection
**Keywords:** "can I", "is it possible", "able to"
**Action:** Check layer boundaries + BRApi restrictions + answer feasibility

---

### D14: Integration Question Detection
**Keywords:** "use X with Y", "connect", "integrate"
**Action:** Check architectural compatibility + provide examples or alternatives

---

### D15: Setup Question Detection
**Keywords:** "how do I create", "how do I setup", "how do I configure"
**Action:** Stay within 1-2 layers; include prerequisites; P3 examples

---

### D16: Calculation Sequence Detection
**Context:** Any calculation question
**Action:** Include sequence context if relevant to understanding behavior

---

### D17: Data Flow Detection
**Keywords:** "from...to", "after", "before", "flow"
**Action:** Multi-layer retrieval following data flow path

---

### D18: Security Context Detection
**Keywords:** "access", "permission", "security", "who can"
**Action:** Include security layers + Workflow interaction

---

### D19: Timing Question Detection
**Keywords:** "when", "timing", "schedule", "frequency"
**Action:** Include Workflow Channels + Process control

---

### D20: Advanced Feature Recognition
**Check for Tier 4-5 concepts**
**Action:** Progressive disclosure + prerequisites + "advanced" flag

---

## Complete Retrieval Algorithm

```python
def intelligent_retrieval(query):
    # PHASE 1: DETECTION
    compound_terms = detect_compound_terms(query)
    exact_identifiers = detect_exact_identifiers(query)
    ambiguous_terms = detect_ambiguous_terms(query)
    layer_signals = detect_layer_signals(query)
    role_signals = detect_role_signals(query)
    pattern_type = detect_query_pattern(query)
    tier_level = detect_concept_tier(query)
    
    # PHASE 2: DISAMBIGUATION
    resolved_terms = {}
    for term in ambiguous_terms:
        context_signals = extract_context_signals(query, term)
        resolved_terms[term] = disambiguate(term, context_signals)
        confidence = get_confidence(term, context_signals)
        if confidence < 0.9:
            mark_for_disambiguation_note(term)
    
    # PHASE 3: PREREQUISITE CHECK
    if tier_level >= 3:
        prerequisites = get_prerequisites(query_concepts)
        user_context = infer_user_knowledge(query)
        gaps = identify_prerequisite_gaps(prerequisites, user_context)
        if gaps:
            include_prerequisites = gaps
    
    # PHASE 4: QUERY EXPANSION
    expanded_query = query
    for rule in inclusion_rules:
        if rule.matches(resolved_terms):
            expanded_query += rule.context_to_include
    # PHASE 4A: EXACT IDENTIFIER LOOKUP
    exact_hits = []
    if exact_identifiers:
        exact_hits = search_api_docs_exact(exact_identifiers)
        expanded_query += extract_embedded_atomic_terms(exact_identifiers)
        if mentions_runtime_parameters(query):
            parameter_context = extract_named_payload_args(exact_hits)
            parameter_context += extract_adjacent_helper_identifiers(exact_hits)
            expanded_query += parameter_context
        if asks_result_shape_or_pov(query):
            result_set_context = extract_cube_view_result_set_surfaces(exact_hits)
            result_set_context += extract_output_schema_helpers(exact_hits)
            expanded_query += result_set_context
    
    # PHASE 5: RETRIEVAL
    results = search_available_docs_or_official_web(expanded_query, n=20)
    results = merge_exact_hits_first(exact_hits, results)
    
    # PHASE 6: POST-PROCESSING
    
    # Apply inclusion rules
    for rule in inclusion_rules:
        if rule.matches(resolved_terms):
            results = add_required_context(results, rule.must_include)
    
    # Apply exclusion rules
    for rule in exclusion_rules:
        if rule.matches(resolved_terms) and not rule.unless_condition(query):
            results = remove_context(results, rule.must_exclude)
    
    # Apply layer boundaries
    primary_layers = get_primary_layers(layer_signals)
    results = filter_by_layers(results, primary_layers, allow_crossing_if(query))
    
    # PHASE 7: PRIORITY SORTING
    results = prioritize(results, {
        'P1': ['definitions', 'direct_answers', 'core_concepts'],
        'P2': ['prerequisites', 'related_concepts', 'context'],
        'P3': ['examples', 'best_practices', 'patterns'],
        'P4': ['alternatives', 'design_patterns', 'tradeoffs'],
        'P5': ['edge_cases', 'advanced', 'detailed_examples']
    })
    
    # PHASE 8: DISAMBIGUATION NOTES
    if has_disambiguation_notes():
        results = add_disambiguation_section(results, resolved_terms)
    
    # PHASE 9: PREREQUISITE GUIDANCE
    if tier_level >= 5:
        results = add_learning_path_guidance(results, prerequisites)
    
    return results
```

---

## Validation Checklist

Before returning results:

**Detection Phase:**
- ✓ Compound terms identified and treated atomically
- ✓ Exact API/member identifiers detected when present
- ✓ Ambiguous terms detected and resolved
- ✓ Layer signals identified
- ✓ Query pattern classified
- ✓ Tier level assessed

**Disambiguation Phase:**
- ✓ Context signals extracted for ambiguous terms
- ✓ Interpretations selected with confidence scores
- ✓ Disambiguation notes flagged if confidence < 90%

**Prerequisite Phase:**
- ✓ Prerequisites identified for advanced topics
- ✓ Knowledge gaps detected
- ✓ Learning path guidance prepared if Tier 5

**Expansion Phase:**
- ✓ Inclusion rules applied
- ✓ Required context added to query

**Retrieval Phase:**
- ✓ Exact lookup executed first for identifier queries
- ✓ Signature-level payload arguments and helper identifiers added for parameter-passing questions
- ✓ Cube View rows/columns/member-filter/POV behavior added for result-shape questions
- ✓ Semantic search executed
- ✓ Results retrieved
- ✓ Exact hits prioritized over loose keyword matches

**Post-Processing Phase:**
- ✓ Inclusion rules applied to results
- ✓ Exclusion rules applied to results
- ✓ Layer boundaries respected
- ✓ Irrelevant context removed

**Priority Phase:**
- ✓ Results sorted P1 → P5
- ✓ Essential concepts prioritized

**Enhancement Phase:**
- ✓ Disambiguation notes added if needed
- ✓ Prerequisite guidance added if Tier 5
- ✓ Learning path provided if appropriate

---

**This rule engine turns source lookup into domain-aware OneStream answering.**
