# Cross References

**Purpose:** Tell an agent which nearby concepts to retrieve together, and which tempting concepts to avoid.

Use this module when source lookup returns scattered results or when the query spans multiple OneStream layers.

## Public References

**Official first:**
- [Cube Views](https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html)
- [Dashboards](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Presentation%20Guides/Dashboards.html)
- [Data Units](https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Workflow%20Guides/Data%20Units.html)
- [Workflow Channels](https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Workflow/NoDataLockCombo.html)
- [Data Access / Slice Security](https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Cube/Data%20Access.html)

**Supplemental public examples:**
- [MindStream Analytics: Linking Cube Views on a Dashboard](https://www.mindstreamanalytics.com/blog/onestream-linking-cube-views-dashboard.html)
- [Perficient: Linked Cube Views and Drill Down](https://blogs.perficient.com/2023/03/21/linked-cube-views-in-onestream-and-drilling-down-to-source-data/)

---

## Topic Clusters

### Cube View Cluster

Always consider:

- Cube View
- POV
- Rows and columns
- Member filters
- Parameters
- Suppression
- Dashboards
- Forms only if data entry is mentioned
- Business Rules only if code, `BR#`, DataCell, or extraction is mentioned

Avoid:

- Generic cube design unless the query is about storage, dimensional model, or performance architecture.

### Dashboard Cluster

Always consider:

- Dashboard components
- Parameters and bound parameters
- Data adapters
- Dashboard DataSet Business Rules
- Cube View components
- User/context values

Avoid:

- Treating dashboard parameters as always identical to cube POV.

### Business Rule Cluster

Always consider:

- Rule type
- `Main` signature
- `SessionInfo`
- `BRGlobals`
- rule-specific `api`
- rule-specific `args`
- BRApi access surface
- invocation context

Avoid:

- Generic programming explanations that ignore OneStream's rule type and execution context.

### FDX / Programmatic Extraction Cluster

Always consider:

- exact method name and containing type
- overload/signature
- return type
- entity/scenario/time filters
- runtime parameter carrier
- Cube View definition and output-shape rules
- dashboard/rule context when used inside a Dashboard DataSet rule

Avoid:

- Answering from Cube View UI configuration alone.

### Workflow Cluster

Always consider:

- Workflow Profile
- Scenario Type
- Time
- Parent/child profile structure
- Workflow Channels
- locks
- certification and confirmation
- data load/calculate/process state

Avoid:

- Treating workflow as only a task list; it controls processing and access context.

### Data Management Cluster

Always consider:

- Data Source
- connector/import process
- Transformation Rules
- Stage validation
- load to cube
- Finance processing after load
- workflow status and locks

Avoid:

- Jumping straight to Finance Business Rules when the problem is pre-load mapping or Stage validation.

### Security Cluster

Always consider:

- security role
- security group
- cube access
- entity/dimensional security
- relationship security
- workflow access
- member display/edit constraints

Avoid:

- Assuming one security setting explains all visibility and editability symptoms.

### Extensible Dimensionality Cluster

Always consider:

- Entity
- UD1-UD8
- EntityDefault members
- cube references
- reporting implications
- data load and consolidation effects

Avoid:

- Suggesting extensibility for dimensions outside the supported dimensionality pattern without verifying documentation.

---

## Source Expansion Rules

### Exact Identifier

If the query has an exact API/member identifier:

1. exact API/member docs
2. containing type/class
3. overloads or sibling methods
4. rule type / execution context
5. concept docs for explanation

### Concept Query

If the query is conceptual:

1. official concept docs
2. architecture/layer module
3. prerequisite module
4. examples or community material as secondary support

### Troubleshooting Query

If the query is troubleshooting:

1. symptom object
2. upstream configuration layer
3. downstream presentation or process layer
4. security/workflow constraints
5. validation steps

---

## Public Search Expansion

When using web search, start with domain-restricted official queries:

```
site:documentation.onestream.com OneStream "Cube Views" "Parameters"
site:documentation.onestream.com OneStream "Workflow Channels"
site:documentation.onestream.com OneStream "Security" "Cube"
site:dev.onestream.com/docs OneStream "Business Rule"
site:dev.onestream.com/docs OneStream "Finance Business Rules"
```

Then widen only if official sources do not answer implementation details.
