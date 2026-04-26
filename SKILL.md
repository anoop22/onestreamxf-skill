# OneStream XF Domain Intelligence Skill

## Purpose

This skill gives AI agents practical domain intelligence for OneStream XF. It helps an agent decide which OneStream reference documents to consult, which concepts to keep together, and how to avoid common terminology traps.

## Public References

**Official first:**
- OneStream Cube Views: `https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html`
- OneStream Cubes: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Cubes.html`
- OneStream Dimensions Overview: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Dimensions%20Overview.html`
- OneStream Business Rule Types: `https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types`
- OneStream API Overview Guide: `https://documentation.onestream.com/1384528/Content/PDFs/API_Overview_Guide.pdf`

**Supplemental public examples:**
- OneStream Community blog: Cube View Style Parameters: `https://community.onestreamsoftware.com/blog/blog/cube-view-style-parameters/1686`
- MindStream Analytics: OneStream Linked Cube Views Overview: `https://www.mindstreamanalytics.com/blog/onestream-linked-cube-views-overview.html`
- Perficient: Building Reports and Dashboards with Parameters: `https://blogs.perficient.com/2022/11/02/onestream-a-simple-guide-to-building-reports-and-dashboards-part-2-of-3-2/`

## What This Skill Does

**Solves the OneStream Context Problem:**
- Prevents concept confusion (for example, using "Cube" docs when the user asks about "Cube View")
- Understands architectural boundaries (when to cross layers vs. stay focused)
- Recognizes prerequisite dependencies (what must be understood first)
- Applies context-aware retrieval rules (what to include/exclude based on query type)
- Disambiguates overloaded terminology (View, Profile, Consolidation, etc.)

## When to Use This Skill

**ALWAYS use when:**
- Processing OneStream XF queries (any subject area: Cubes, Consolidation, Workflow, Data Management, Calculations, Reporting)
- Deciding what context to retrieve alongside matched documents
- Resolving ambiguous technical terms
- Determining if prerequisites are needed
- Reviewing reference-document results before answering

**Module Selection Strategy:**
1. Start with `0-quick-reference.md` for common patterns
2. Use specialized modules as needed for deep analysis
3. Apply retrieval rules before returning results to user

## Skill Architecture

This skill uses a **modular design** to keep context efficient:

```
SKILL.md (this file)
├── 0-quick-reference.md          [Fast lookup for 80% of queries]
├── 1-conceptual-architecture.md  [Complete concept taxonomy]
├── 2-compound-terms.md           [Atomic terms that shouldn't split]
├── 3-architectural-layers.md     [Layer boundaries & interaction rules]
├── 4-prerequisites.md            [Knowledge dependency chains]
├── 5-disambiguations.md          [Resolving ambiguous terminology]
├── 6-query-patterns.md           [Question type → retrieval strategy]
├── 7-domain-logic.md             [Business rules & constraints]
├── 8-cross-references.md         [Context expansion rules]
├── 9-retrieval-rules.md          [Complete rule engine]
└── 10-public-web-resources.md    [Official public source map]
```

## Quick Start Guide

### For Simple Queries (80% of cases)

**Read:** `0-quick-reference.md` only

This covers:
- Pattern recognition (10 common question types)
- Fast disambiguation (View, Profile, Consolidation, etc.)
- Top 20 inclusion/exclusion rules
- Common confusions quick fixes

### For Complex Queries

**Sequential approach:**

1. **Pattern Detection** → `0-quick-reference.md` (identify question type)
2. **Disambiguation** → `5-disambiguations.md` (if ambiguous terms detected)
3. **Architecture Check** → `3-architectural-layers.md` (determine layer boundaries)
4. **Prerequisite Scan** → `4-prerequisites.md` (if advanced topics detected)
5. **Retrieval Rules** → `9-retrieval-rules.md` (apply full rule engine)

### For Architectural Questions

**Read:** `1-conceptual-architecture.md` + `3-architectural-layers.md`

### For Terminology Confusion

**Read:** `2-compound-terms.md` + `5-disambiguations.md`

### For Learning Path Guidance

**Read:** `4-prerequisites.md` (complete dependency chains)

### For Exact API / BRApi Questions

**Read:** `0-quick-reference.md` + `2-compound-terms.md` + `9-retrieval-rules.md`

Use this path when the query contains an exact identifier such as `FdxExecuteCubeView`:
- Exact-match the identifier in API docs first
- Preserve embedded atomic terms such as `Cube View`
- Use owner type, signature, and nearby APIs to infer documented purpose
- If the question is about passing runtime parameters, expand exact lookup to the named payload argument and nearby helper/context identifiers (`*Args`, `NameValuePairs`, builder/formatter types) before broad concept search
- Treat loose keyword matches as secondary evidence only

Also use this path when a concept query clearly implies programmatic execution even if the API name is missing.
- Example: `sample code to extract data from a Cube View`
- Promote likely exact identifiers from the concept/action pair before broad source search
- Retrieve rule context types, signatures, and return types before writing code
- Use concept docs only to explain parameters, filters, and surrounding setup

### For Public Reference Answers

**Read:** `0-quick-reference.md` + `6-query-patterns.md` + `10-public-web-resources.md`

Use this path when the agent is relying on OneStream reference documents and public citations:
- Search official OneStream documentation and the OneStream Developer Portal first
- Prefer exact API/member references over broad concept pages for code questions
- Use community or partner sources only as secondary hints
- Cite the public sources used and mark version-sensitive details
- If exact API evidence is not public, give a validation path inside OneStream

## Core Intelligence Concepts

### 1. Compound Terms (Don't Split)
OneStream has 45+ multi-word technical terms that are **conceptually atomic**:
- "Cube View" ≠ "Cube" (different architectural layers)
- "Workflow Profile" ≠ generic "Profile" (specific configuration object)
- "Member Formula" ≠ generic "Formula" (calculation type)

**See:** `2-compound-terms.md` for complete list

### 2. Architectural Layers (Boundary Rules)
7 functional layers with specific interaction rules:
- Foundation → Metadata → Data Collection → Workflow → Calculation → Business Rules → Presentation
- Know when to cross boundaries vs. stay focused

**See:** `3-architectural-layers.md` for interaction matrix

### 3. Prerequisite Dependencies (Learning Paths)
27 concepts organized into 6 tiers (0-5):
- Advanced concepts require understanding lower tiers first
- 6 role-based learning chains (End User, Admin, Analyst, Developer, Architect)

**See:** `4-prerequisites.md` for complete graph

### 4. Common Confusions (Disambiguation Logic)
15 critical ambiguities documented:
- "View" has 4+ meanings (Cube View, IC View, Input View, SQL View)
- "Consolidation" has 3 meanings (Process, Members, Dimension)
- "Profile" has 2 meanings (Workflow Profile, Time Profile)

**See:** `5-disambiguations.md` for resolution rules

### 5. Retrieval Rules (Intelligence Engine)
55+ explicit rules:
- 20 INCLUSION rules ("when X, always include Y")
- 15 EXCLUSION rules ("don't mix X with Y unless...")
- 20 DISAMBIGUATION rules ("if ambiguous, check for signals")

**See:** `9-retrieval-rules.md` for complete rule engine

## Usage Workflow

### Pre-Processing (Before Retrieval)

```python
1. Read: 0-quick-reference.md
2. Detect exact API/member identifiers (if present)
3. Detect pattern type (How to, Why, Difference, etc.)
4. Identify ambiguous terms
5. Check for disambiguation signals
6. Expand query with prerequisites (if advanced topic)
```

### Retrieval Source Order

```python
1. Exact API/member docs, if available
2. Official OneStream product documentation
3. OneStream Developer Portal for Business Rule/extensibility topics
4. Public community/partner examples as secondary evidence
```

### Post-Processing (After Retrieval)

```python
1. Apply INCLUSION rules (add missing context)
2. Apply EXCLUSION rules (remove irrelevant results)
3. Check prerequisite gaps (surface if needed)
4. Sort by priority (P1 concepts before P5 examples)
5. Add disambiguation notes (if ambiguous terms detected)
```

## Example: Intelligent Retrieval in Action

### User Query
"How do I create a Cube View?"

### Without Domain Intelligence
Loose document matching may return:
- Cube View documentation ✓
- Cube documentation ✗ (matched only because of "Cube")
- View documentation ✗ (matched only because of "View")
- Mixed results from different layers ✗

### With Domain Intelligence

**Step 1: Pattern Detection** (`0-quick-reference.md`)
- Pattern: "How do I create" → Setup/Configuration question

**Step 2: Disambiguation** (`5-disambiguations.md`)
- "Cube View" is atomic term → don't retrieve general "Cube" or "View"

**Step 3: Prerequisite Check** (`4-prerequisites.md`)
- Cube View requires: Cube, Dimension Members (Tier 1 prerequisites)

**Step 4: Apply Inclusion Rules** (`9-retrieval-rules.md`)
- Include: Member Filters, Parameters (common co-occurrence)

**Step 5: Apply Exclusion Rules** (`9-retrieval-rules.md`)
- Exclude: Form details (different layer unless "data entry" mentioned)

**Final Retrieval:**
1. Cube View definition and structure (P1)
2. Cube structure basics (P2 - prerequisite)
3. Dimension Members (P2 - prerequisite)
4. Member Filters (P3 - common with Cube Views)
5. Parameters (P3 - common with Cube Views)
6. Cube View examples (P5)

**Also Surface:** Disambiguation note if user might confuse with "Cube"

## Critical Reminders

### Always Check for Ambiguity
OneStream terminology is heavily overloaded:
- View, Profile, Rule, Formula, Consolidation, Unit, Cell, Member

**Before retrieving**, consult disambiguation rules.

### Respect Architectural Boundaries
Don't mix layers unless query explicitly spans them:
- Presentation layer (Cube Views) ≠ Data Collection layer (Forms)
- Calculation layer (Member Formulas) ≠ Workflow layer (Profiles)

**Check layer interaction rules** in `3-architectural-layers.md`

### Include Prerequisites for Advanced Topics
If user queries advanced concepts without prerequisites:
- Surface prerequisite concepts first
- Provide learning path guidance
- Don't assume prior knowledge

**Consult prerequisite chains** in `4-prerequisites.md`

### Apply Compound Term Rules
45+ terms should never be split:
- "Cube View" is ONE concept
- "Workflow Profile" is ONE concept
- "Member Formula" is ONE concept

**Reference complete list** in `2-compound-terms.md`

## Module Loading Strategy

### Minimal Context (Fast)
For 80% of queries, only load:
- `0-quick-reference.md` (small)

### Moderate Context (Balanced)
For queries needing disambiguation or prerequisites:
- `0-quick-reference.md`
- `5-disambiguations.md` (if ambiguous)
- `4-prerequisites.md` (if advanced topic)

### Full Context (Comprehensive)
For complex architectural or multi-concept queries:
- Load relevant specialized modules as needed
- Never load all 10 modules at once (unnecessary context consumption)

## Success Metrics

This skill improves OneStream answer quality by:

**Precision:**
- Eliminates irrelevant concept matches (Cube vs Cube View)
- Reduces false positives from overloaded terminology

**Recall:**
- Includes prerequisite concepts automatically
- Adds co-occurring context via inclusion rules

**User Experience:**
- Provides disambiguation when terms are ambiguous
- Surfaces learning paths for advanced topics
- Answers follow-up questions preemptively

## Maintenance

### When to Update
- New OneStream versions introduce concepts
- Queries reveal unhandled patterns
- User feedback shows confusion points
- Performance tuning needed

### How to Update
1. Analyze new documentation
2. Update affected modules
3. Re-validate retrieval rules
4. Test with sample queries

## Agent Usage Flow

This skill is designed to work out of the box when an agent can load these files and consult OneStream reference documents:

```
User Query
    ↓
[Load 0-quick-reference.md]
    ↓
[Detect pattern + disambiguate]
    ↓
[Load specialized modules if needed]
    ↓
[Expand query with prerequisites]
    ↓
[Consult OneStream reference documents and official public sources]
    ↓
[Apply inclusion/exclusion rules]
    ↓
[Sort by priority]
    ↓
[Add disambiguation notes]
    ↓
Return grounded OneStream answer
```

## Quick Reference Card

**For Fast Lookup:**
- Common patterns → `0-quick-reference.md`
- Ambiguous term → `5-disambiguations.md` 
- Compound term check → `2-compound-terms.md`
- Advanced topic → `4-prerequisites.md`
- Full rule engine → `9-retrieval-rules.md`

**For Deep Analysis:**
- Architecture → `1-conceptual-architecture.md`
- Layer boundaries → `3-architectural-layers.md`
- Query strategies → `6-query-patterns.md`
- Business rules → `7-domain-logic.md`
- Context expansion → `8-cross-references.md`
- Public web sources → `10-public-web-resources.md`

---

## Module Descriptions

### 0-quick-reference.md
**Fast lookup for common scenarios**
- 10 query pattern templates
- Top 10 inclusion/exclusion rules
- Disambiguation quick fixes
- Decision trees for common questions
- Emergency disambiguation guide

### 1-conceptual-architecture.md
**Complete OneStream taxonomy**
- 27 core concepts with definitions
- Hierarchical relationships (parent/child/peer)
- 7 architectural layers
- "Distinct from" clarifications
- Visual concept tree

### 2-compound-terms.md
**Terms that shouldn't split**
- 45+ atomic multi-word terms
- "Why atomic" explanations
- "What NOT to confuse with" rules
- Retrieval rules for each term

### 3-architectural-layers.md
**Layer boundaries & interaction rules**
- 7 functional layers defined
- When to cross vs. stay within layers
- Layer-specific retrieval guidance
- Cross-layer interaction matrix

### 4-prerequisites.md
**Knowledge dependency chains**
- 27 concepts in 6 tiers (0-5)
- 6 role-based learning paths
- Backward dependency rules
- Complete prerequisite mapping

### 5-disambiguations.md
**Resolving ambiguous terminology**
- 15 critical ambiguities
- Context signal detection
- Disambiguation decision trees
- Warning signals table

### 6-query-patterns.md
**Question type → retrieval strategy**
- 10 common question patterns
- Required understanding for each
- What to retrieve for each type
- Follow-up question chains

### 7-domain-logic.md
**Business rules & constraints**
- 20+ IF/THEN rules
- "When X, consider Y" table
- Architecture constraints
- Performance implications

### 8-cross-references.md
**Context expansion rules**
- 10 topic clusters
- "Always reference together" rules
- External knowledge assumptions
- Prerequisite documents

### 9-retrieval-rules.md
**Complete rule engine**
- 20 INCLUSION rules
- 15 EXCLUSION rules  
- 20 DISAMBIGUATION rules
- 5-tier priority system
- Complete synthesis of all rules

### 10-public-web-resources.md
**Official public source map**
- OneStream documentation starting points
- OneStream Developer Portal starting points
- Domain-restricted search templates
- Public-source citation and uncertainty rules

---

**This skill helps OneStream agents move from keyword matching to domain-aware retrieval and public-source research.**

Start with `0-quick-reference.md` for immediate impact, then expand to specialized modules as needed.
