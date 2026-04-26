# Public Web Resources

**Purpose:** Help an agent answer OneStream questions when it only has this skill plus web access.

Use official OneStream sources first. Use community or partner material only as secondary evidence.

---

## Source Priority

1. **Official OneStream documentation** for product concepts, configuration, security, workflow, dashboards, and Cube Views.
2. **OneStream Developer Portal** for Business Rule standards, extensibility patterns, and developer guidance.
3. **Official PDFs and versioned guides** when HTML pages are not enough.
4. **OneStream Community / partner blogs / examples** only for implementation hints, and label them as non-authoritative.
5. **Model memory** only after sources are checked; mark uncertainty.

---

## Official Documentation Map

Use these pages as starting points:

- Presentation overview: `https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Presentation/Presentation.html`
- Cube Views: `https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube%20Views/Build%20Reports%20through%20Cube%20Views.html`
- Dashboards: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Presentation%20Guides/Dashboards.html`
- Cubes: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Cubes.html`
- Dimensions Overview: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Cube/Dimensions%20Overview.html`
- Configurable Dimensions: `https://documentation.onestream.com/docs/Content/Design%20and%20Reference/Cube/Configurable%20Dimensions.html`
- Member Script Constants: `https://documentation.onestream.com/8.5.1/Content/Design%20and%20Reference/Cube/Member%20Script%20Constants.html`
- Data Units: `https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Workflow%20Guides/Data%20Units.html`
- Workflow Channels: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Workflow/NoDataLockCombo.html`
- Data Access / Slice Security: `https://documentation.onestream.com/8.4.0/Content/Design%20and%20Reference/Cube/Data%20Access.html`
- Security Configurations: `https://documentation.onestream.com/1389761/Content/Design%20and%20Reference/Foundation%20Guides/Security%20Configurations.html`
- API Overview Guide PDF: `https://documentation.onestream.com/1384528/Content/PDFs/API_Overview_Guide.pdf`

Some URLs are versioned examples. If answering a current-production question, search for the same page title under the user's OneStream version.

---

## Developer Portal Map

Use these pages as starting points for developer and Business Rule questions:

- Business Rule Types: `https://dev.onestream.com/docs/solution-exchange/dev-standards/components/business-rule-types`
- Finance Business Rules: `https://dev.onestream.com/docs/solution-exchange/dev-standards/finance-business-rules`
- Development Standards: `https://dev.onestream.com/docs/category/development-standards`
- Components: `https://dev.onestream.com/docs/category/components`
- Coding Standards and Practices: `https://dev.onestream.com/docs/solution-exchange/dev-standards/coding-standards-and-practices`
- Solution Core Requirements: `https://dev.onestream.com/docs/solution-exchange/solution-creation/core-requirements`

Developer portal pages often describe standards and patterns rather than complete API signatures. For exact signatures, prefer API reference material when available.

---

## Search Templates

### Concept or UI Topic

```
site:documentation.onestream.com OneStream "<concept>"
site:documentation.onestream.com "Design and Reference" "OneStream" "<concept>"
```

### Cube View / Dashboard

```
site:documentation.onestream.com "Cube Views" "Parameters" "OneStream"
site:documentation.onestream.com "Dashboards" "Data Adapter" "OneStream"
site:documentation.onestream.com "Bound Parameters" "Cube View" "OneStream"
```

### Workflow / Security

```
site:documentation.onestream.com "Workflow Channels" "OneStream"
site:documentation.onestream.com "Workflow Profile" "Scenario" "Time" "OneStream"
site:documentation.onestream.com "Security" "Cube Access" "OneStream"
```

### Business Rules / API

```
site:dev.onestream.com/docs "Business Rule Types" "OneStream"
site:dev.onestream.com/docs "Finance Business Rules" "OneStream"
site:documentation.onestream.com "API Overview Guide" "OneStream"
```

### Exact Identifier

```
"FdxExecuteCubeView" "OneStream"
"DashboardDataSetArgs" "OneStream"
"FinanceRulesArgs" "OneStream"
"NameValuePairs" "OneStream"
```

---

## Public-Source Answering Rules

- Cite the official source used.
- Mention the source version when visible in the URL or page.
- Do not present community code as official API guidance.
- If exact API docs are unavailable publicly, say so and provide a validation path in OneStream's rule editor/API browser.
- Keep the answer useful: explain the likely pattern, then separate verified facts from implementation assumptions.
