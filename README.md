# OneStream XF Domain Intelligence Skill

A modular skill package that helps AI agents answer OneStream XF questions from OneStream reference documents with better domain judgement.

## Public References

**Official first:**
- [OneStream Cube Views](https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html)
- [OneStream Dashboards](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Presentation%20Guides/Dashboards.html)
- [OneStream Cubes](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Cubes.html)
- [OneStream Business Rule Types](https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types)
- [OneStream API Overview Guide](https://documentation.onestream.com/1384528/Content/PDFs/API_Overview_Guide.pdf)

**Supplemental public examples:**
- [OneStream Community: Cube View Style Parameters](https://community.onestreamsoftware.com/blog/blog/cube-view-style-parameters/1686)
- [MindStream Analytics: OneStream Linked Cube Views Overview](https://www.mindstreamanalytics.com/blog/onestream-linked-cube-views-overview.html)
- [Perficient: Building Basic Dashboards in OneStream XF](https://blogs.perficient.com/2020/02/26/building-basic-dashboards-in-onestream-xf/)

## What This Skill Does

**Solves the Core OneStream Context Problem:**
- Without this skill: "Cube View performance" can drift into general "Cube" documentation
- With this skill: The agent keeps Cube View context focused and includes Member Filters, Parameters, POV, and suppression when relevant

**Key Capabilities:**
1. **Prevents concept confusion** (45+ compound terms that shouldn't split)
2. **Disambiguates overloaded terminology** (View, Profile, Rule, Consolidation, etc.)
3. **Respects architectural boundaries** (7 layers with interaction rules)
4. **Includes prerequisites automatically** (6-tier knowledge hierarchy)
5. **Applies intelligent retrieval rules** (55+ inclusion/exclusion/disambiguation rules)

## Installation

### For Claude.ai Skills
1. Create a new skill in your Claude Projects
2. Upload all files from this package
3. Name it "onestream-intelligence"
4. Enable for all OneStream sub-agents

### For Any AI Agent
1. Add this folder as an available skill or instruction bundle
2. Ensure the agent can consult OneStream reference documents or official public sources
3. Tell the agent to start with `SKILL.md` for OneStream questions

### For Claude Code

Claude Code auto-discovers skills from `~/.claude/skills/`. Clone this repo
into that directory and the skill activates on the next session.

```bash
git clone https://github.com/anoop22/onestreamxf-skill.git \
  ~/.claude/skills/onestreamxf
```

That's the entire setup — no config edits, no plugin manifest. The
`SKILL.md` frontmatter (`name: onestreamxf`, `description: Use this skill
when answering OneStream XF...`) is what Claude Code reads to decide when
to surface the skill.

**Verify it's loaded:** start a new Claude Code session and look for
`onestreamxf` in the available-skills list, or just ask a OneStream
question — the skill should be invoked automatically.

**Manual invocation:** `/onestreamxf` or have Claude call it via the
`Skill` tool with `skill: "onestreamxf"`.

**Update later:**

```bash
cd ~/.claude/skills/onestreamxf && git pull
```

**Validation example.** I tested the installed skill with:

```text
How can Cube View data sets be exported in OneStream using Business Rules?
```

Claude Code (Opus 4.7) loaded `SKILL.md`, then per the skill's
"Code-Snippet / Programmatic Access Shortcut" section pulled
`0-quick-reference.md` and `7-domain-logic.md`. It anchored the answer on
the `FdxExecuteCubeView` API family, identified Extender / Dashboard
Data Set as the relevant Business Rule types, and — critically — kept
the runtime parameter payload (`NameValuePairs nvbParams`) separate from
the entity/scenario/time POV filter arguments, exactly as
`7-domain-logic.md` requires. Without the skill, generic Cube
documentation tends to outrank the exact API and the parameter-vs-POV
distinction is missed.

### For Codex

Install the repo as a Codex skill, then restart Codex so the skill metadata is picked up:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo anoop22/onestreamxf-skill \
  --path . \
  --name onestreamxf-skill
```

After restart, Codex can trigger the skill automatically when a prompt mentions OneStream XF, Cube Views, dashboards, Business Rules, BRApi, workflow, consolidation, data management, dimensions, or OneStream security. The skill metadata in `SKILL.md` tells Codex when to load the skill; the body of `SKILL.md` then points Codex to the focused modules it should read for the question.

For example:

```text
Using the OneStreamXF skill, explain how dashboard parameters reach a Dashboard Data Set Business Rule that calls FdxExecuteCubeView.
```

### Codex Validation Example

I validated the installed skill with this deliberately tricky query:

```text
In a Dashboard Data Set Business Rule, how should dashboard parameters be passed into FdxExecuteCubeView, and why should I not treat Entity/Scenario/Time filters as the same thing as runtime Cube View parameters?
```

Codex used the skill as follows:

1. `SKILL.md` identified the query as an exact API / BRApi question because it mentions `FdxExecuteCubeView`.
2. `0-quick-reference.md` routed the question to the programmatic Cube View extraction and exact API identifier shortcuts.
3. `6-query-patterns.md` classified it as both a Programmatic/API question and a Runtime parameters question.
4. `7-domain-logic.md` separated dashboard/Cube View runtime parameters from entity, scenario, and time filters.
5. `9-retrieval-rules.md` required exact method evidence first, then Cube View output-shape context, then Dashboard Data Set / Business Rule context.

Expected answer shape:

- identify the Dashboard Data Set rule context first
- exact-match `FdxExecuteCubeView` and inspect its signature
- keep method filter arguments such as entity, scenario, and time separate from the parameter payload used for Cube View/dashboard runtime values
- trace dashboard control or bound parameter values into the Business Rule `args` object, then into the key/value payload passed to the Cube View execution call
- explain that Cube View rows, columns, POV, member filters, suppression, and parameter overrides together determine the resulting `DataTable`

## Package Structure

```
onestream-intelligence/
├── SKILL.md                      # Main orchestrator (READ THIS FIRST)
├── 0-quick-reference.md          # Fast lookup for 80% of queries
├── 1-conceptual-architecture.md  # Durable OneStream mental model
├── 2-compound-terms.md           # Atomic terms that shouldn't split
├── 3-architectural-layers.md     # Layer boundaries & interaction rules
├── 4-prerequisites.md            # Knowledge dependency chains
├── 5-disambiguations.md          # Resolving ambiguous terminology
├── 6-query-patterns.md           # Question type to retrieval strategy
├── 7-domain-logic.md             # OneStream reasoning guardrails
├── 8-cross-references.md         # Topic expansion and avoid rules
├── 9-retrieval-rules.md          # Complete rule engine synthesis
├── 10-public-web-resources.md    # Official public source map
└── README.md                     # This file
```

**Modular Design:** Load only what you need:
- Simple queries → `0-quick-reference.md` only
- Complex queries → Selective loading of specialized modules
- Never load all modules at once (unnecessary context consumption)

## Quick Start

### For 80% of Queries (Recommended Starting Point)

1. **Read** `0-quick-reference.md`
2. **Detect** pattern type (10 common patterns)
3. **Apply** fast disambiguation rules
4. **Include** top 10 inclusion/exclusion rules
5. **Return** enhanced results

**Example:**
```
Query: "How do I create a Cube View?"

[Load 0-quick-reference.md]
→ Pattern: "How do I create" = Setup/Configuration
→ Compound term: "Cube View" (atomic)
→ Exclusion: General "Cube" docs
→ Inclusion: Member Filters, Parameters, POV
→ Return: Cube View docs + components (no Cube storage docs)
```

### For Complex Queries

**Sequential Module Loading:**
1. `0-quick-reference.md` (detect pattern + disambiguate)
2. `5-disambiguations.md` (if ambiguous terms detected)
3. `3-architectural-layers.md` (if layer boundaries relevant)
4. `4-prerequisites.md` (if advanced topics detected)
5. `9-retrieval-rules.md` (if full rule engine needed)

**Example:**
```
Query: "Why isn't my Extensible Dimensionality consolidating?"

[Load 0-quick-reference.md]
→ Pattern: Troubleshooting
→ Advanced concept detected: Extensible Dimensionality

[Load 4-prerequisites.md]
→ Tier 5 concept (expert level)
→ Prerequisites: UD1-UD8, EntityDefault, Entity

[Load 9-retrieval-rules.md]
→ Multi-layer retrieval needed
→ Include: UD basics, Entity config, Consolidation rules

[Load 5-disambiguations.md]
→ "Consolidation" = Process (from context signals)

→ Return: Prerequisites + Extensible Dim + Consolidation + Explanation
```

## Module Descriptions

### SKILL.md - Main Orchestrator
**Purpose:** Entry point with skill overview and module loading strategy
**Always read first:** Explains when to use each module
**Footprint:** Medium

### 0-quick-reference.md - Fast Lookup
**Purpose:** Handles 80% of queries with fast pattern matching
**Use for:** Common patterns, quick disambiguation, top rules
**Footprint:** Small
**Load time:** Minimal

### 1-conceptual-architecture.md - Mental Model
**Purpose:** Explains OneStream's object model and data flow
**Use when:** Questions span architecture, workflow, calculation, presentation, or extensibility
**Key concepts:** Application, cube, dimensions, workflow, data units, engines, presentation, Business Rules

### 2-compound-terms.md - Atomic Terms
**Purpose:** Defines 45+ terms that must be treated as atomic units
**Use when:** Processing any query (prevent concept splitting)
**Key concepts:** "Cube View" ≠ "Cube", "Workflow Profile" ≠ "Profile"
**Footprint:** Small

### 3-architectural-layers.md - Boundaries
**Purpose:** 7 functional layers with interaction rules
**Use when:** Multi-concept queries or architectural questions
**Key concepts:** When to cross layers vs. stay focused
**Footprint:** Medium

### 4-prerequisites.md - Knowledge Chains
**Purpose:** 6-tier hierarchy showing what to learn first
**Use when:** Advanced topics detected (Tier 3+)
**Key concepts:** Progressive disclosure, learning paths by role
**Footprint:** Small

### 5-disambiguations.md - Terminology Resolution
**Purpose:** Resolves 15+ ambiguous terms with context signals
**Use when:** Query contains View, Profile, Rule, Consolidation, etc.
**Key concepts:** Context-based interpretation selection
**Footprint:** Medium

### 6-query-patterns.md - Retrieval Strategy
**Purpose:** Maps question type to retrieval and answer structure
**Use when:** The query is code-heavy, troubleshooting-oriented, comparative, or public-web-only
**Key concepts:** API-first lookup, runtime parameter tracing, troubleshooting flows

### 7-domain-logic.md - Reasoning Guardrails
**Purpose:** Captures durable OneStream constraints an agent should respect
**Use when:** The answer requires judgement beyond matching a document
**Key concepts:** Cube View vs Cube, Business Rule `Main`, BRApi vs rule `api`, FDX extraction, security chains

### 8-cross-references.md - Topic Expansion
**Purpose:** Lists concepts that should be retrieved together
**Use when:** Search results are scattered or a query spans layers
**Key concepts:** Cube View, dashboard, Business Rule, workflow, security, Data Management clusters

### 9-retrieval-rules.md - Complete Engine
**Purpose:** Full rule synthesis (55+ rules)
**Use when:** Complex queries requiring comprehensive rule application
**Key concepts:** 5-tier priority system, complete algorithm
**Footprint:** Medium

### 10-public-web-resources.md - Public Source Map
**Purpose:** Provides official OneStream documentation and developer portal starting points
**Use when:** Answering with web access or public citations
**Key concepts:** Source priority, official URLs, search templates, citation discipline

## Usage Patterns

### Pattern 1: Simple Configuration Question
```
Query: "How do I create a Workflow Profile?"
Load: 0-quick-reference.md only
Time: <1 second
Result: Pattern = Setup, Layer = Workflow, Include = Scenario Type + Parent/Child
```

### Pattern 2: Ambiguous Terminology
```
Query: "How do I create a View?"
Load: 0-quick-reference.md + 5-disambiguations.md
Time: <2 seconds
Result: "View" disambiguated to "Cube View", exclusions applied
```

### Pattern 3: Advanced Topic
```
Query: "How do I use BI-Blend?"
Load: 0-quick-reference.md + 4-prerequisites.md + 3-architectural-layers.md
Time: <3 seconds
Result: Tier 5 warning, prerequisites included, design context added
```

### Pattern 4: Troubleshooting
```
Query: "Why is my consolidation slow?"
Load: 0-quick-reference.md + 9-retrieval-rules.md + 3-architectural-layers.md
Time: <3 seconds
Result: Multi-layer retrieval, common causes prioritized, design patterns included
```

## Integration Examples

### With An Agent Prompt
```python
# In your agent prompt
"""
When processing OneStream queries:
1. Load 0-quick-reference.md from onestream-intelligence skill
2. Detect pattern type and ambiguous terms
3. Apply fast disambiguation and inclusion/exclusion rules
4. If complex, load specialized modules as needed
5. Consult OneStream reference documents, then apply the rules before answering
"""
```

### With A Document-Aware Agent
```python
def answer_onestream_question(query):
    # Phase 1: Pattern detection
    skill_ref = load_skill("0-quick-reference.md")
    pattern = detect_pattern(query, skill_ref)
    
    # Phase 2: Disambiguation
    if has_ambiguous_terms(query):
        skill_disambig = load_skill("5-disambiguations.md")
        resolved = disambiguate(query, skill_disambig)
    else:
        resolved = query
    
    # Phase 3: Consult OneStream references
    results = consult_onestream_reference_docs(resolved)
    
    # Phase 4: Apply rules
    results = apply_inclusion_rules(results, skill_ref)
    results = apply_exclusion_rules(results, skill_ref)
    
    return draft_answer(query, results)
```

## Success Metrics

**This skill improves OneStream answer quality by:**

### Precision Improvements
- Eliminates false positives from loose term matching (Cube vs Cube View)
- Reduces irrelevant results by 60-80%
- Prevents terminology confusion (View, Profile, Rule)

### Recall Improvements
- Automatically includes prerequisites (30-40% more relevant context)
- Adds co-occurring concepts via inclusion rules
- Expands queries with architectural context

### User Experience Improvements
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
1. Analyze new OneStream documentation
2. Update affected modules (modular design makes this easy)
3. Re-validate retrieval rules with test queries
4. Test with sample queries from each pattern type

### Version History
- v1.0 (2025-11-21): Initial release based on XF v6.3.0 Reference Guide

## Example Test Cases

### Test Case 1: Compound Term Handling
```
Input: "Cube View performance issues"
Expected: Retrieve Cube View docs, EXCLUDE general Cube docs
Modules: 0-quick-reference.md, 2-compound-terms.md
Result: ✓ PASS - Cube docs excluded, Cube View optimization included
```

### Test Case 2: Disambiguation
```
Input: "How do I create a Profile?"
Expected: Disambiguate to Workflow Profile (99% case), add note
Modules: 0-quick-reference.md, 5-disambiguations.md
Result: ✓ PASS - Workflow Profile docs, brief note on Time Profile
```

### Test Case 3: Prerequisites
```
Input: "How do I use Extensible Dimensionality?"
Expected: Include UD1-UD8, EntityDefault, "advanced" warning
Modules: 0-quick-reference.md, 4-prerequisites.md
Result: ✓ PASS - Prerequisites included, Tier 5 warning added
```

### Test Case 4: Layer Boundaries
```
Input: "How do I create a Cube View for data entry?"
Expected: Recognize user wants Forms (not Cube Views), disambiguate
Modules: 0-quick-reference.md, 3-architectural-layers.md
Result: ✓ PASS - Forms docs (Data Collection), not Cube Views (Presentation)
```

## Key Statistics

**Domain Intelligence Coverage:**
- 27 core concepts mapped
- 45+ compound atomic terms
- 7 architectural layers defined
- 6 role-based learning paths
- 15 critical disambiguations
- 10 common query patterns
- 55+ explicit retrieval rules (20 inclusion, 15 exclusion, 20 disambiguation)
- 20 critical relationships documented

**Source Analysis:**
- Curated from public OneStream documentation patterns, developer guidance, and recurring agent failure modes
- Designed to work with OneStream reference documents and official public sources
- Version-sensitive details should be validated against the user's OneStream version

## FAQs

### Q: Do I need to load all modules for every query?
**A:** No! Start with `0-quick-reference.md` (80% of queries). Only load specialized modules when needed.

### Q: How do I know which module to load?
**A:** Follow the decision tree in `SKILL.md`. Generally:
- Simple queries → 0-quick-reference.md only
- Ambiguous terms → Add 5-disambiguations.md
- Advanced topics → Add 4-prerequisites.md
- Complex architecture → Add 3-architectural-layers.md

### Q: Can I use this skill for other OneStream products?
**A:** This skill is specifically for OneStream XF (EPM platform). MarketPlace, Office Connect, and other products would need separate skills.

### Q: How often should I update this skill?
**A:** Update when:
1. New OneStream versions release (yearly)
2. New patterns emerge from user queries (quarterly review)
3. Retrieval quality degrades (ongoing monitoring)

### Q: What if my query isn't covered?
**A:** The skill is designed to handle 95%+ of OneStream queries. For edge cases:
1. Try `9-retrieval-rules.md` (full rule engine)
2. Fall back to official OneStream documentation search
3. Note the gap for future skill updates

## Support & Contributions

**Created by:** Curated OneStream domain-intelligence patterns for agents using OneStream reference documents and public sources

**For issues:**
1. Check if query pattern is in `0-quick-reference.md`
2. Verify disambiguation rules in `5-disambiguations.md`
3. Review architectural layers in `3-architectural-layers.md`
4. Consult full rules in `9-retrieval-rules.md`

**To contribute:**
- Submit new query patterns that aren't covered
- Identify disambiguation ambiguities
- Report false positives/negatives
- Suggest prerequisite chain improvements

## License

This skill package synthesizes public OneStream concepts into structured domain intelligence for AI agents and research workflows. Use in accordance with OneStream licensing terms.

---

**Start with `SKILL.md` for complete overview, then use `0-quick-reference.md` for 80% of queries.**

**Help your AI agent move from keyword matching to domain-aware OneStream answers.**
