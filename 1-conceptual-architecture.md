# Conceptual Architecture

**Purpose:** Give an agent a durable mental model of OneStream before it retrieves or answers.

Use this module when the user asks architectural, design, "how does this fit together", or multi-layer questions.

## Public References

**Official first:**
- Cubes: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Cubes.html`
- Dimensions Overview: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Dimensions%20Overview.html`
- Data Units: `https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Workflow%20Guides/Data%20Units.html`
- Cube Views: `https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html`
- Business Rule Types: `https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types`

**Supplemental public examples:**
- MindStream Analytics: Linked Cube Views Overview: `https://www.mindstreamanalytics.com/blog/onestream-linked-cube-views-overview.html`
- Perficient: Linked Cube Views and Drill Down: `https://blogs.perficient.com/2023/03/21/linked-cube-views-in-onestream-and-drilling-down-to-source-data/`

---

## The Minimum Mental Model

OneStream is an EPM platform where structured financial data moves through a predictable chain:

```
Application
  -> Cube and dimensions
  -> Members and hierarchies
  -> Workflow and data collection
  -> Stage / Finance processing
  -> Calculations and consolidation
  -> Cube Views, dashboards, reports, forms
  -> Business Rules and APIs for extension
```

Most bad answers happen when an agent jumps to the wrong layer:

- A **Cube** stores dimensional financial data.
- A **Cube View** presents or queries cube data; it is not the cube itself.
- A **Form** is the data-entry experience and often uses Cube View layout concepts.
- A **Workflow Profile** controls process scope and status.
- A **Data Unit** is the calculation/process scope, usually tied to workflow, scenario, and time.
- A **Business Rule** is VB.NET-based extension logic whose available context depends on rule type.

---

## Core Object Taxonomy

### Foundation Objects

| Concept | Agent definition | Do not confuse with |
|---------|------------------|---------------------|
| Application | The OneStream solution container | A single cube or environment |
| Cube | Dimensional storage and processing model | Cube View/report layout |
| Dimension | Axis of analysis such as Account, Entity, Scenario, Time, Flow, Origin, IC, UD dimensions | A member |
| Member | A node inside a dimension hierarchy | A dimension itself |
| Security Group | Access-control assignment unit | Workflow status or locks |

### Operational Objects

| Concept | Agent definition | Retrieval implication |
|---------|------------------|-----------------------|
| Workflow Profile | Defines process structure, input/review flow, and often data-unit scope | Include scenario/time/status/locks when relevant |
| Data Source | Defines imported source data shape | Include transformation and Stage context |
| Transformation Rule | Maps or changes imported data before cube load | Keep separate from Business Rules unless the query spans both |
| Form | Data entry surface | Include Cube View only as layout/input context |
| Cube View | Presentation/query surface for cube data | Include member filters, parameters, POV, suppression |

### Calculation and Extension Objects

| Concept | Agent definition | Retrieval implication |
|---------|------------------|-----------------------|
| Member Formula | Calculation attached to a member | Include dynamic vs stored behavior |
| Consolidation | Processing that aggregates/translates/eliminates data according to entity/currency/intercompany rules | Include Data Unit, entity hierarchy, consolidation members |
| Business Rule | Rule-type-specific VB.NET extension entry point | Retrieve rule type, `Main` signature, `api`/`args` types |
| BRApi | Shared API surface exposed to Business Rules | Do not collapse with the rule-specific `api` parameter |
| Dashboard DataSet Rule | Business Rule type used to return tabular data to dashboard components | Include `DashboardDataSetArgs` and parameter handling |

---

## Data Flow Model

Use this when troubleshooting or explaining "where does this value come from?"

1. **Metadata defines shape:** Dimensions, members, hierarchies, properties, cube references.
2. **Workflow controls process:** Profiles, channels, status, locks, certification, confirmation.
3. **Data enters:** Forms, imports, connectors, Data Management sequences.
4. **Stage validates and maps:** Data sources and transformation rules prepare data before load.
5. **Finance processing loads/calculates:** Cube data, member formulas, Business Rules, consolidations.
6. **Presentation reads data:** Cube Views, dashboards, reports, books, extensible documents.
7. **Business Rules extend behavior:** Rule type determines available `api`, `args`, and execution timing.

Do not answer a troubleshooting question from only the final symptom. Trace the flow backward until the first layer that can explain the issue.

---

## Layer Boundary Rules

### Stay Narrow When

- The query names a single exact API/member identifier.
- The query asks for a definition.
- The query is about one configuration object and has no cross-layer signal.
- The answer depends on a rule signature, method overload, or exact parameter name.

### Cross Layers When

- The query says "not working", "wrong value", "after load", "when", "security", "dashboard parameter", "BR#", "DataCell", or "from cube view to datatable".
- The question joins presentation and code, such as Cube View extraction through a Business Rule.
- The question joins workflow and calculations, such as consolidation timing, locking, or certification.
- The question joins security and visibility, such as members not appearing in Cube Views or forms.

---

## Source Discipline

When answering from retrieved material or web resources:

1. Prefer official OneStream documentation and developer portal pages.
2. Prefer exact API/member docs over broad concept pages when code is requested.
3. Use community, partner, or blog content only as secondary implementation hints.
4. Mark version-specific details when the source version is visible.
5. If evidence is thin, state the uncertainty and give a validation step inside OneStream.

---

## Agent Answer Shape

For OneStream answers, a good response usually includes:

- The direct answer first.
- The OneStream object/layer involved.
- Any rule type, method, or exact parameter name that matters.
- The configuration path or code pattern if the user asked "how".
- A validation checklist for troubleshooting questions.
- Source/version caveats when using public web material.
