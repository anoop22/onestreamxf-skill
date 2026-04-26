# Query Patterns

**Purpose:** Map user question type to retrieval strategy and answer structure.

Use this module after `0-quick-reference.md` when the query is complex, code-heavy, ambiguous, or troubleshooting-oriented.

---

## Pattern Table

| Pattern | Signals | Retrieve first | Answer shape |
|---------|---------|----------------|--------------|
| Definition | "what is", "explain", "meaning" | Exact concept page, glossary-like source | Direct definition, layer, distinct-from |
| Configuration | "how do I create/configure/setup" | Object docs, prerequisites, UI/config path | Steps, required prerequisites, gotchas |
| Programmatic/API | code, BRApi, method name, DataTable, snippet | Exact API/member docs, owner type, signature | Signature, rule context, sample pattern, caveats |
| Runtime parameters | parameter, prompt, dashboard, NameValuePairs, `BR#`, `args` | Caller syntax plus receiving rule args | End-to-end value path |
| Troubleshooting | why, error, not working, wrong value | Multi-layer flow around symptom | Likely causes ordered by layer, checks |
| Comparison | vs, difference, should I use | Both concepts and boundary rules | Decision table and default recommendation |
| Feasibility | can I, is it possible | Boundary rules, rule/API restrictions | Yes/no/depends, constraints, alternative |
| Performance/design | slow, optimize, large, design | Design pattern, data-unit/report scope | Diagnosis, tradeoffs, measurement points |
| Security/visibility | access, permission, missing member/data | Security docs, cube/workflow/dimension access | Access chain and validation steps |
| Learning path | new to, teach me, overview | Prerequisite tiers, architecture | Progressive path, what to learn next |

---

## Programmatic/API Questions

Use this path when the user asks for code or names an API-like identifier.

1. Exact-match the identifier first.
2. Retrieve owner class/type, namespace, signature, return type, overloads, and examples.
3. Retrieve the Business Rule type that can legally call the API.
4. Retrieve argument carrier types such as `*Args`, `NameValuePairs`, or rule-specific APIs.
5. Only then retrieve broad concept docs to explain why the method behaves that way.

### Example: Cube View to DataTable

If the user asks how to pull Cube View data into a `DataTable`, route to:

- `FdxExecuteCubeView` family
- containing import/data API type
- signature argument that carries dashboard/runtime parameters
- `DashboardDataSetArgs` if the caller is a Dashboard DataSet rule
- Cube View rows, columns, member filters, POV, parameters, suppression

Do not answer only with Cube View design docs. The method signature is the P1 evidence.

---

## Runtime Parameter Questions

Use this path when the user asks how dashboard prompts, Cube View parameters, `BR#`, or Business Rule `args` values are passed.

Retrieve both sides of the handoff:

- caller syntax or dashboard component configuration
- receiving Business Rule type
- `Main` signature for that rule type
- concrete `*Args` class and relevant child property
- any key/value carrier such as `NameValuePairs`

Answer with a trace:

```
Dashboard / Cube View value
  -> caller payload or parameter binding
  -> Business Rule Main parameter
  -> args child object / key lookup
  -> API call or returned value
```

---

## Troubleshooting Questions

For "wrong value", "not showing", "locked", or "slow" questions, retrieve the minimum path that could produce the symptom.

### Wrong Cube View Value

Check:

1. Cube View POV, rows, columns, and member filters.
2. Parameters and dashboard-bound values.
3. View/Scenario/Time/Entity context.
4. Member formula or Business Rule calculation.
5. Consolidation status and Data Unit scope.
6. Security and workflow locks if visibility or editability is involved.

### Import/Load Problem

Check:

1. Workflow profile and scenario/time.
2. Data Source and connector settings.
3. Transformation Rules.
4. Stage validation.
5. Load step and Finance processing.
6. Confirmation rules and locks.

### Security/Visibility Problem

Check:

1. Application/security role.
2. Cube access.
3. Entity and dimensional security.
4. Workflow profile access.
5. Display member group or member visibility.
6. Whether the issue is read, write, execute, or certify access.

---

## Public Web Answering Pattern

When no documentation index is available:

1. Search official OneStream documentation first.
2. Search the OneStream Developer Portal for Business Rule and extensibility topics.
3. Search public community or partner resources only after official sources.
4. Quote sparingly; paraphrase and link sources.
5. Clearly mark assumptions and version-sensitive steps.

Use `10-public-web-resources.md` for source maps and search templates.

