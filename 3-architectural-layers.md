# Architectural Layers & Boundaries

**Purpose:** Define OneStream's functional layers and rules for when to cross boundaries vs. stay focused.

**Critical:** Understanding layer boundaries prevents mixing unrelated concepts during retrieval.

## Public References

**Official first:**
- [Cubes](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Cubes.html)
- [Dimensions Overview](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Dimensions%20Overview.html)
- [Data Units](https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Workflow%20Guides/Data%20Units.html)
- [Workflow Channels](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Workflow/NoDataLockCombo.html)
- [Business Rule Types](https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types)

**Supplemental public examples:**
- [MindStream Analytics: Linked Cube Views Overview](https://www.mindstreamanalytics.com/blog/onestream-linked-cube-views-overview.html)
- [OneStream Community: About Advanced Reporting and Dashboards](https://community.onestreamsoftware.com/kb/onestream-press-excerpts/about-advanced-reporting-and-dashboards/45613)

---

## The 7 Functional Layers

```
┌─────────────────────────────────────────┐
│  7. PRESENTATION LAYER                  │  ← User-facing reporting
│     (Cube Views, Dashboards)            │
├─────────────────────────────────────────┤
│  6. BUSINESS RULES LAYER                │  ← Custom logic
│     (Business Rules, Extensions)        │
├─────────────────────────────────────────┤
│  5. CALCULATION LAYER                   │  ← Core calculations
│     (Consolidation, Translation,        │
│      Member Formulas)                   │
├─────────────────────────────────────────┤
│  4. WORKFLOW LAYER                      │  ← Process control
│     (Workflow Profiles, Certification,  │
│      Locking, Channels)                 │
├─────────────────────────────────────────┤
│  3. DATA COLLECTION LAYER               │  ← Data entry & import
│     (Forms, Data Management,            │
│      Stage/Finance Engines)             │
├─────────────────────────────────────────┤
│  2. METADATA LAYER                      │  ← Structure definition
│     (Dimensions, Members, Hierarchies)  │
├─────────────────────────────────────────┤
│  1. FOUNDATION LAYER                    │  ← Core architecture
│     (Cube, Security, Application)       │
└─────────────────────────────────────────┘
```

---

## Layer Definitions & Scope

### Layer 1: Foundation
**Components:**
- Application structure
- Cube definition (18 dimensions)
- Security Groups
- Cube Access rules
- Relationship Security

**Scope:** Infrastructure and architecture
**Interacts with:** All layers (foundation for everything)
**Stay focused when:** Query is purely architectural

---

### Layer 2: Metadata
**Components:**
- Dimensions (Account, Entity, Scenario, Time, etc.)
- Dimension Members
- Hierarchies (parent-child relationships)
- Member Properties
- Dimension structure

**Scope:** Data structure and organization
**Interacts with:** All layers above (all use metadata)
**Stay focused when:** Query is about dimension structure only

---

### Layer 3: Data Collection
**Components:**
- Forms (data entry)
- Form Templates
- Form Child Profiles
- Data Management (import/ETL)
- Data Sources
- Transformation Rules
- Stage Engine (validation)

**Scope:** Getting data INTO the system
**Interacts with:**
- Foundation (uses Cube structure)
- Metadata (populates Members)
- Workflow (controlled by Profiles)
- Calculation (data flows to calculations)

**Stay focused when:** Query is about data entry OR import, not both
**Cross to Workflow when:** "validation", "approval" mentioned
**Cross to Calculation when:** "after load calculation" mentioned

---

### Layer 4: Workflow
**Components:**
- Workflow Profiles (Data Unit scope)
- Parent/Child Workflow Profiles
- Workflow Channels (timing)
- Certification
- Confirmation Rules
- Locking
- Workflow Status

**Scope:** Process control and timing
**Interacts with:**
- Data Collection (controls data entry)
- Calculation (controls calculation timing)
- Presentation (controls data visibility)

**Stay focused when:** Query is about process/approval flow
**Cross to Calculation when:** "calculation timing" mentioned
**Cross to Data Collection when:** "data entry process" mentioned

---

### Layer 5: Calculation
**Components:**
- Consolidation Process
- Consolidation Members (Top, Share, Elimination)
- Member Formulas
- Translation (currency)
- Elimination (intercompany)
- Data Units (calculation scope)
- Calculation sequence

**Scope:** Core financial calculations
**Interacts with:**
- Workflow (triggered by Workflow timing)
- Business Rules (custom calculation logic)
- Presentation (calculated results displayed)

**Stay focused when:** Query is purely calculation mechanics
**Cross to Workflow when:** "when does calculation run" mentioned
**Cross to Business Rules when:** "complex logic" mentioned
**Cross to Presentation when:** "display results" mentioned

---

### Layer 6: Business Rules
**Components:**
- Business Rule Types (Calculate, Consolidate, etc.)
- BRApi (programming interface)
- Event Handlers
- Extenders
- Complex Expressions
- External DLL integration

**Scope:** Custom extensibility and logic
**Interacts with:**
- Calculation (called during calculations)
- Data Collection (Finance Engine)
- Workflow (Event Handlers)
- Presentation (custom Cube View `BR#` / DataCell handlers)

**Stay focused when:** Query is about VB.NET code or BRApi
**Cross to Calculation when:** Understanding what Business Rule calculates
**Cross to Data Collection when:** "after load" mentioned (Finance Engine)
**Cross to Presentation when:** `GetDataCell("BR#[...]")`, custom data-cell logic, or Cube View rendering mentioned

---

### Layer 7: Presentation
**Components:**
- Cube Views (read-only display)
- Dashboards
- Extensible Documents
- Excel Add-in
- Parameters
- Member Filters
- Suppression rules
- Formatting

**Scope:** User-facing reporting and visualization
**Interacts with:**
- Calculation (displays calculated data)
- Data Collection (Forms use Cube Views for layout)
- Workflow (respects locking/security)
- Business Rules (custom `BR#`-backed data cells)

**Stay focused when:** Query is purely about display/formatting
**Cross to Data Collection when:** "data entry" mentioned (Forms, not Cube Views)
**Cross to Calculation when:** Understanding what's being displayed
**Cross to Business Rules when:** `GetDataCell("BR#[...]")`, `FinanceFunctionType.DataCell`, `DataCellArgs`, `FunctionName`, `NameValuePairs`, or custom dynamic calc logic mentioned

---

## Layer Interaction Rules

### When to Cross Layers

| Current Layer | Cross To | When Query Contains |
|--------------|----------|-------------------|
| Foundation | Workflow | "how is data controlled", "process" |
| Foundation | Security | "who can access", "permission" |
| Metadata | Calculation | "how are members calculated" |
| Metadata | Data Collection | "how are members populated" |
| Data Collection | Workflow | "validation", "approval", "timing" |
| Data Collection | Calculation | "after load", "Finance Engine" |
| Workflow | Calculation | "calculation timing", "when consolidate" |
| Workflow | Data Collection | "data entry process", "lock forms" |
| Calculation | Business Rules | "complex logic", "VB.NET", "custom" |
| Calculation | Presentation | "display", "report", "view results" |
| Business Rules | Calculation | "what does this calculate" |
| Business Rules | Presentation | `GetDataCell("BR#[...]")`, "custom data cell", "Cube View rendering" |
| Presentation | Data Collection | "data entry" (switch to Forms) |
| Presentation | Business Rules | `BR#[`, `GetDataCell`, `FinanceFunctionType.DataCell`, `DataCellArgs`, or "custom dynamic calc" |

### When to Stay Within Layer

| Layer | Stay Focused When |
|-------|------------------|
| Foundation | "Cube structure", "architecture", "security model" |
| Metadata | "dimension design", "hierarchy", "member properties" |
| Data Collection | "import process" OR "data entry" (but not both at once) |
| Workflow | "approval flow", "certification", "process control" |
| Calculation | "consolidation algorithm", "translation", "Member Formula" |
| Business Rules | "BRApi syntax", "code example", "Event Handler" |
| Presentation | "report formatting", "Cube View design", "suppression" |

---

## Boundary Rules by Query Type

### "How do I..." Queries

**Pattern:** Setup/Configuration

**Strategy:** Usually stay within 1-2 layers

**Examples:**
- "How do I create a Cube View?" → **Presentation only** (don't cross to Calculation unless "what to display")
- "How do I pass parameters from a Cube View to a Finance rule?" → **Presentation + Business Rules** (Cube View `BR#[...]` caller syntax + `FinanceFunctionType.DataCell` / `DataCellArgs`)
- "How do I setup workflow?" → **Workflow only** (don't cross to Calculation unless "timing")
- "How do I load data?" → **Data Collection only** (don't cross to Calculation unless "after load")

### "Why is my..." Queries

**Pattern:** Troubleshooting

**Strategy:** Often requires crossing layers (follow data flow)

**Examples:**
- "Why is my consolidation slow?" → **Calculation + Workflow + Foundation** (Data Units, timing, Cube design)
- "Why isn't my data loading?" → **Data Collection + Workflow** (Transformation Rules, validation, locking)
- "Why can't I see data?" → **Presentation + Workflow + Foundation** (Cube View, security, suppression)

### "What's the difference..." Queries

**Pattern:** Comparison

**Strategy:** May cross layers if comparing concepts from different layers

**Examples:**
- "Cube vs Cube View?" → **Foundation vs Presentation** (architectural difference)
- "Member Formula vs Business Rule?" → **Calculation vs Business Rules** (calculation mechanisms)
- "Stage Engine vs Finance Engine?" → **Data Collection** (both in same layer)

### "Can I..." Queries

**Pattern:** Feasibility/Constraints

**Strategy:** Check layer constraints and cross-layer compatibility

**Examples:**
- "Can I call BRApi from Stage Engine?" → **NO** (Business Rules layer not accessible from Data Collection)
- "Can I use Member Formula in Cube View?" → **YES** (Calculation flows to Presentation)
- "Can I lock Forms with Workflow?" → **YES** (Workflow controls Data Collection)

---

## Layer Crossing Matrix

| From ↓ / To → | Foundation | Metadata | Data Collection | Workflow | Calculation | Business Rules | Presentation |
|---------------|-----------|----------|----------------|----------|-------------|---------------|-------------|
| **Foundation** | - | Always | Via Workflow | Always | Via Workflow | Via Calc | Via Calc |
| **Metadata** | Always | - | Always | Always | Always | Always | Always |
| **Data Collection** | Via structure | Via population | - | Via control | Via engine | Via Finance | NO* |
| **Workflow** | Via config | Via filter | Via control | - | Via timing | Via events | Via security |
| **Calculation** | Via design | Via formulas | NO | Via timing | - | Via BRApi | Via results |
| **Business Rules** | Via code | Via API | Via Finance | Via events | Via calc | - | Via Cube View BR#* |
| **Presentation** | Via security | Via selection | Via Forms* | Via access | Via display | Via Cube View BR#* | - |

**Legend:**
- **Always:** Direct relationship, cross freely
- **Via X:** Indirect relationship through intermediary
- **NO:** Cannot directly interact (architectural boundary)
- ***Caveat:** Forms use Cube Views for layout (Data Collection → Presentation), and Cube Views can invoke Finance rule `DataCell` logic through `GetDataCell("BR#[...]")` as a specialized Presentation ↔ Business Rules bridge

---

## Common Layer Violations to Prevent

### ❌ Mixing Cube View with Forms
**Wrong:** "How do I create a Cube View for data entry?"
**Right:** "How do I create a Form for data entry?" (Forms, not Cube Views)
**Retrieval:** Data Collection layer (Forms), NOT Presentation (Cube Views)

### ❌ Mixing Member Formula with Business Rule
**Wrong:** "Should I use Member Formula or Business Rule?" (treating as equivalent)
**Right:** "Member Formula (Calculation layer) vs Business Rule (Business Rules layer)"
**Retrieval:** Explain layer difference + when to use each

### ❌ BRApi in Stage Engine
**Wrong:** "Can I call BRApi from Transformation Rule?"
**Right:** "BRApi is only accessible from Finance Engine, not Stage Engine"
**Retrieval:** Explain layer boundary + alternative approaches

### ❌ Dynamic Calc in Consolidation sequence
**Wrong:** "Why isn't my Dynamic Member Formula consolidating?"
**Right:** "Dynamic calcs don't participate in Consolidation Process"
**Retrieval:** Explain Dynamic vs Stored + Consolidation sequence

---

## Signal Words by Layer

### Foundation Layer Signals
**Words:** "architecture", "structure", "security", "Cube design", "application"
**Retrieve:** Cube types, Security model, Architecture patterns

### Metadata Layer Signals
**Words:** "dimension", "member", "hierarchy", "parent-child", "property"
**Retrieve:** Dimension structure, Member configuration, Hierarchies

### Data Collection Layer Signals
**Words:** "import", "load", "ETL", "transform", "data entry", "form"
**Retrieve:** Data Management OR Forms (not both unless query spans)

### Workflow Layer Signals
**Words:** "approval", "certification", "lock", "process", "timing", "channel"
**Retrieve:** Workflow Profiles, Certification, Locking, Channels

### Calculation Layer Signals
**Words:** "calculate", "consolidate", "translate", "formula", "algorithm"
**Retrieve:** Consolidation, Translation, Member Formulas, Sequence

### Business Rules Layer Signals
**Words:** "VB.NET", "code", "BRApi", "custom logic", "Event Handler"
**Retrieve:** Business Rule types, BRApi, Programming concepts

### Presentation Layer Signals
**Words:** "report", "display", "dashboard", "view", "format", "chart"
**Retrieve:** Cube Views, Dashboards, Parameters, Formatting

---

## Retrieval Strategy by Layer

### Single-Layer Queries
**Strategy:** Stay focused, minimal context from other layers

**Example:** "How do I suppress rows in Cube View?"
**Layers:** Presentation only
**Include:** Suppression rules, Member Filters, Dynamic Calc (related)
**Exclude:** Workflow, Data Management, Business Rules

### Two-Layer Queries
**Strategy:** Primary layer + supporting layer

**Example:** "How do I lock Forms based on Workflow?"
**Layers:** Workflow (primary) + Data Collection (Forms)
**Include:** Locking mechanism, Workflow Profile, Form interaction
**Exclude:** Calculation, Presentation, Business Rules

### Multi-Layer Queries
**Strategy:** Follow data flow through layers

**Example:** "How does data flow from import to report?"
**Layers:** Data Collection → Workflow → Calculation → Presentation
**Include:** Complete flow, transitions between layers
**Exclude:** Business Rules (unless custom logic mentioned)

---

## Validation Checklist

Before returning retrieval results:

- ✓ Identified primary layer from query signals
- ✓ Determined if layer crossing is needed
- ✓ Applied stay-focused rules if single-layer query
- ✓ Applied interaction rules if multi-layer query
- ✓ Excluded layers with NO interaction (prevented violations)
- ✓ Verified layer-appropriate context included

---

**Understanding layer boundaries is key to focused, accurate retrieval.**
