# Domain Logic Rules

**Purpose:** Capture durable OneStream reasoning rules that should guide answers even before retrieval.

These are not replacement documentation. They are guardrails that keep an agent from making common OneStream mistakes.

## Public References

**Official first:**
- Cube Views: `https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html`
- Dashboards: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Presentation%20Guides/Dashboards.html`
- Data Access / Slice Security: `https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Cube/Data%20Access.html`
- BRApi: `https://documentation.onestream.com/1388457/Content/Design%20and%20Reference/Foundation%20Guides/BRApi.html`
- Business Rule Types: `https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types`

**Supplemental public examples:**
- OneStream Community: FdxExecuteCubeView parameters: `https://community.onestreamsoftware.com/discussions/WorkflowDI/fdxexecutecubeview-parameters/13514`
- MindStream Analytics: Conditional Cell Formatting with XFBR: `https://www.mindstreamanalytics.com/blog/onestream-cube-view-multi-column-conditional-variance-formatting.html`

---

## Presentation and Data Entry

### Cube View vs Cube

If the user says **Cube View**, treat it as a presentation/query object, not storage.

- Include member filters, POV, rows, columns, parameters, suppression, and dashboard usage.
- Exclude cube design/storage unless the user asks about cube structure or performance design.

### Forms vs Cube Views

If the user asks for **data entry**, consider Forms even if they say Cube View.

- Cube Views define display/query layout.
- Forms are the data-entry workflow surface.
- Some form behavior uses Cube View concepts, so include Cube View only as supporting context.

---

## Business Rule Execution

### Standard Main Shape

All Business Rules have a `Main` entry point pattern with stable and rule-type-specific parameters:

```vbnet
Public Function Main(ByVal si As SessionInfo,
                     ByVal globals As BRGlobals,
                     ByVal api As Object,
                     ByVal args As <RuleSpecificArgs>) As Object
```

The exact `api` and `args` types vary by Business Rule type. Do not explain `args` generically without identifying the rule type.

### `BRApi` vs `api`

- `BRApi` is the broader shared API namespace/surface used inside Business Rules.
- `api` is the rule-specific parameter passed into `Main`.
- `args` is a parameter variable whose declared type depends on the rule type.

When asked "is `args` a class/function/namespace?", answer by separating:

- variable name: `args`
- declared type: for example `FinanceRulesArgs` or `DashboardDataSetArgs`
- runtime value: the object instance passed when OneStream invokes the rule
- namespace/class container: only if the documentation identifies it

---

## Cube View Runtime Logic

### Dashboard Parameters

If a Cube View is used in a dashboard, parameter values can be supplied by dashboard controls, bound parameters, or caller code. Trace the value from the UI/control to the Cube View or API call rather than assuming it is in the POV.

### `BR#` / DataCell Handoff

If a Cube View calls a Business Rule through `BR#` / DataCell syntax:

1. The Cube View expression is the caller.
2. The Finance Business Rule receives a DataCell-oriented invocation.
3. The relevant payload is under the Finance rule `args` object, commonly through a DataCell child argument object and key/value pairs.
4. Values can come from the current cell intersection, explicit key/value payloads, or dimensions overridden inside the rule.

Keep those sources separate in the answer.

---

## FDX and Cube View Extraction

When the user asks to extract Cube View results programmatically:

- Prefer exact API documentation for the `FdxExecuteCubeView` family.
- Identify required filters such as entity, scenario, and time arguments.
- Identify the runtime parameter payload argument separately from entity/scenario/time filters.
- Explain output shape through Cube View rows, columns, member filters, POV, and suppression.
- Mention adjacent helper APIs only if supported by documentation or the user's context.

Do not invent hidden columns, POV-only modes, or return schemas without evidence.

---

## Workflow, Data Units, and Locks

If the query involves workflow status, load, calculate, certify, lock, or unlock:

- Include Workflow Profile.
- Include Scenario and Time.
- Include Data Unit if calculation or processing scope matters.
- Include Workflow Channel when timing or partial-lock behavior is involved.
- Include security if a user cannot see, edit, process, certify, or unlock something.

---

## Security Reasoning

Do not answer security questions from a single permission flag.

OneStream access commonly depends on a chain:

```
User / group
  -> role permissions
  -> cube access
  -> dimensional or relationship security
  -> workflow profile access
  -> member display/edit constraints
```

For "I can see X but cannot do Y", identify whether Y is read, write, execute, process, certify, or administer access.

---

## Calculation Reasoning

For calculation questions, determine which calculation mechanism is involved:

- Member Formula: member-attached logic, dynamic or stored.
- Business Rule: reusable code invoked by a rule type or workflow/process.
- Consolidation: entity hierarchy, ownership/share/elimination, translation, Data Unit scope.
- Dynamic calculation: calculated on retrieval/display path and may not behave like stored consolidation data.

If the question is "why doesn't it consolidate?", check whether the logic participates in consolidation or only evaluates dynamically.

---

## Version and Evidence Rules

- API signatures and rule types are version-sensitive: verify exact names.
- UI labels and navigation can change by version: answer with concept plus likely path.
- Public examples may omit security, workflow, or scenario/time context: add those caveats.
- If sources disagree, prefer official docs and label community content as illustrative.
