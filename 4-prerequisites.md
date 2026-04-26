# Prerequisites - Knowledge Dependency Chains

**Purpose:** Define what concepts must be understood FIRST before tackling advanced topics.

**Critical:** Prevents providing advanced documentation without foundational context.

---

## The 6-Tier Knowledge Hierarchy

```
Tier 0: FOUNDATION CONCEPTS (must understand first)
  ->
Tier 1: STRUCTURAL CONCEPTS (build on foundation)
  ->
Tier 2: OPERATIONAL CONCEPTS (use structure)
  ->
Tier 3: ADVANCED FEATURES (extend operations)
  ->
Tier 4: INTEGRATION CONCEPTS (connect systems)
  ->
Tier 5: EXPERT CONCEPTS (complex scenarios)
```

---

## Complete Concept Hierarchy

### Tier 0: Foundation (Start Here)

**Concepts:**
1. **Application** - OneStream container
2. **Cube** - Data storage structure with 18 dimensions
3. **Dimension** - Organizational axis (Account, Entity, Scenario, Time, etc.)
4. **Member** - Individual element within Dimension

**Prerequisites for Tier 0:** None (entry point)

**Required before moving to Tier 1:** Understand:
- Cube contains Dimensions
- Dimensions contain Members
- Members organize data hierarchically

---

### Tier 1: Structural (Build on Foundation)

**Concepts:**
5. **Dimension Member** - Specific Member with properties
6. **Hierarchy** - Parent-child Member relationships
7. **Scenario Type** - Actual/Budget/Forecast classification
8. **Time Dimension** - Temporal organization
9. **Account Dimension** - Chart of accounts
10. **Entity Dimension** - Organizational units
11. **User Defined Dimensions (UD1-UD8)** - Custom dimensions

**Prerequisites:** Tier 0 (must understand Dimension and Member first)

**Required before moving to Tier 2:** Understand:
- How Members form hierarchies
- How Scenario Type affects behavior
- How Time periods work
- Basic dimension structure

---

### Tier 2: Operational (Use Structure)

**Concepts:**
12. **Workflow Profile** - Defines Data Unit scope
13. **Data Unit** - Calculation scope (Profile + Scenario + Time)
14. **Cube View** - Display/query mechanism
15. **Form** - Data entry mechanism
16. **Member Formula** - Member-level calculation
17. **Consolidation Process** - Calculation execution
18. **Data Source** - External data connection
19. **Transformation Rule** - ETL logic

**Prerequisites:** Tier 0 + Tier 1 (structure must exist before operations)

**Required before moving to Tier 3:** Understand:
- How Workflow Profiles define scope
- How Data Units are calculated
- How Cube Views display data
- How Forms enable data entry
- Basic calculation concepts

---

### Tier 3: Advanced Features (Extend Operations)

**Concepts:**
20. **Business Rule** - Custom VB.NET logic
21. **BRApi** - Programming interface for Business Rules
22. **Consolidation Members** - Top, Share, Elimination
23. **Translation** - Currency conversion
24. **Elimination** - Intercompany removal
25. **Member Filters** - Cube View data selection
26. **Parameters** - Cube View variables
27. **Workflow Channels** - Timing control

**Prerequisites:** Tier 0 + Tier 1 + Tier 2 (operational concepts must be understood)

**Required before moving to Tier 4:** Understand:
- When to use Business Rules vs Member Formulas
- How consolidation algorithms work
- How translation affects calculations
- How Member Filters work

---

### Tier 4: Integration (Connect Systems)

**Concepts:**
28. **Data Management** - Full ETL system
29. **Stage Engine** - Pre-load validation
30. **Finance Engine** - Post-load calculation
31. **Dashboard** - Visualization integration
32. **Extensible Document** - Document integration

**Prerequisites:** Tier 0 + Tier 1 + Tier 2 + Tier 3

**Required before moving to Tier 5:** Understand:
- Complete data flow (Stage → Finance → Calculation)
- How systems integrate
- When to use each component

---

### Tier 5: Expert (Complex Scenarios)

**Concepts:**
33. **Extensible Dimensionality** - Dynamic dimension expansion
34. **Standard Large Sparse** - Design for sparse data > 750k cells
35. **Hybrid Cube** - Dual storage pattern
36. **BI-Blend** - Aggregation design
37. **Relational Blending** - SQL pass-through
38. **Event Handlers** - Advanced Business Rule type
39. **Extenders** - External DLL integration

**Prerequisites:** ALL previous tiers (expert-level requires full system understanding)

---

## Role-Based Learning Paths

### For End Users (Read-Only Access)

**Path:**
```
1. Dimension (Tier 0)
   ->
2. Member (Tier 0)
   ->
3. Cube (Tier 0)
   ->
4. Cube View (Tier 2)
   ->
5. Dashboard (Tier 4)
```

**Estimated Learning Time:** 2-4 hours

**Skip:** Workflow, Calculations, Data Management, Business Rules

---

### For Data Entry Users

**Path:**
```
1. Dimension (Tier 0)
   ->
2. Member (Tier 0)
   ->
3. Cube (Tier 0)
   ->
4. Workflow Profile (Tier 2)
   ->
5. Form (Tier 2)
   ->
6. Data Unit (Tier 2) [understand why data locks]
```

**Estimated Learning Time:** 4-8 hours

**Skip:** Calculations (unless entering formulas), Business Rules, Advanced features

---

### For Administrators

**Path:**
```
1. Dimension (Tier 0)
   ->
2. Cube (Tier 0)
   ->
3. Workflow Profile (Tier 2)
   ->
4. Data Source (Tier 2)
   ->
5. Transformation Rule (Tier 2)
   ->
6. Data Management (Tier 4)
   ->
7. Stage Engine (Tier 4)
```

**Estimated Learning Time:** 16-24 hours

**Skip:** Advanced calculations (unless also Analyst role)

---

### For Analysts

**Path:**
```
1. Dimension (Tier 0)
   ->
2. Member (Tier 0)
   ->
3. Account (Tier 1)
   ->
4. Hierarchy (Tier 1)
   ->
5. Member Formula (Tier 2)
   ->
6. Consolidation Process (Tier 2)
   ->
7. Consolidation Members (Tier 3)
   ->
8. Translation (Tier 3)
   ->
9. Elimination (Tier 3)
```

**Estimated Learning Time:** 20-32 hours

**Focus:** Calculation concepts and financial logic

---

### For Developers

**Path:**
```
1. Dimension (Tier 0)
   ->
2. Cube (Tier 0)
   ->
3. Member Formula (Tier 2)
   ->
4. Consolidation (Tier 2)
   ->
5. BRApi (Tier 3)
   ->
6. Business Rule (Tier 3)
   ->
7. Finance Engine (Tier 4)
   ->
8. Complex Expression (Tier 3)
   ->
9. Event Handlers (Tier 5)
   ->
10. Extenders (Tier 5)
```

**Estimated Learning Time:** 40-60 hours

**Focus:** Programming and extensibility

---

### For Architects

**Path:**
```
1. Cube (Tier 0)
   ->
2. Dimensions (all) (Tier 0-1)
   ->
3. Workflow Profile (Tier 2)
   ->
4. Data Unit (Tier 2)
   ->
5. Consolidation (Tier 2)
   ->
6. Cube Design Patterns (Tier 5)
   ->
7. Standard Large Sparse (Tier 5)
   ->
8. Hybrid Cube (Tier 5)
   ->
9. BI-Blend (Tier 5)
   ->
10. Extensible Dimensionality (Tier 5)
```

**Estimated Learning Time:** 60-80 hours

**Focus:** Architecture, design patterns, performance

---

## Backward Dependency Rules

**"If researching [X], must understand [Y] first"**

### Consolidation Process
**Prerequisites:**
- Data Unit (what's being calculated)
- Workflow Profile (what defines Data Unit)
- Scenario Type (affects calculation behavior)
- Entity Hierarchy (consolidation structure)
- Members (what's being consolidated)

### Business Rule
**Prerequisites:**
- Member Formula (simpler alternative to understand first)
- BRApi (programming interface)
- Consolidation (when Business Rules execute)
- Data Unit (calculation context)

### Data Management
**Prerequisites:**
- Data Source (what's being imported)
- Transformation Rule (how data is modified)
- Stage Engine (validation before load)
- Cube structure (where data goes)
- Dimensions (how data is organized)

### Cube View
**Prerequisites:**
- Cube (what's being displayed)
- Dimension Members (what's being selected)
- Member Filters (how to select)
- Parameters (how to parameterize)

### Extensible Dimensionality
**Prerequisites:**
- User Defined Dimensions (UD1-UD8) (what can be extended)
- Entity Dimension (primary extensible dimension)
- EntityDefault Members (default values)
- Reporting implications (how it affects queries)
- **ALL Tier 0-2 concepts** (expert-level feature)

### BI-Blend
**Prerequisites:**
- Standard Cube (what's being aggregated)
- Data Unit (performance context)
- Cube Design Patterns (alternative approaches)
- **ALL Tier 0-2 concepts** (expert design pattern)

---

## Prerequisite Detection Signals

**If query contains these terms, check for prerequisite gaps:**

| Advanced Term | Required Prerequisites | Tier |
|--------------|----------------------|------|
| Extensible Dimensionality | UD1-UD8, EntityDefault, Entity | 5 |
| BI-Blend | Standard Cube, Data Unit, Performance | 5 |
| Relational Blending | Cube, SQL, Data Sources | 5 |
| Event Handler | Business Rule, BRApi, Workflow | 5 |
| Standard Large Sparse | Cube Design, Data Unit, Sparsity | 5 |
| Business Rule | Member Formula, BRApi, Consolidation | 3 |
| Translation | Consolidation, FX Rates, Members | 3 |
| Elimination | Consolidation, IC, Entity Hierarchy | 3 |
| Data Management | Data Source, Transformation Rule | 4 |
| Finance Engine | Business Rule, Data loading | 4 |

---

## Query Expansion Based on Prerequisites

### Example 1: Advanced Topic Without Prerequisites

**Query:** "How do I use Extensible Dimensionality?"

**Prerequisite check:** Tier 5 concept requires Tiers 0-4

**Expansion strategy:**
1. **Alert user:** "Extensible Dimensionality is an advanced feature. Prerequisites:"
2. Provide Tier 0-1 basics: Dimension, Member, UD1-UD8
3. Provide Tier 2 context: EntityDefault, Entity Dimension
4. Provide Tier 5 detail: Extensible Dimensionality itself
5. Include Tier 3 context: Reporting implications

**Retrieval priority:**
- P1: Prerequisites (Tier 0-1)
- P2: Context (Tier 2)
- P1: Actual query (Tier 5)
- P3: Related implications

---

### Example 2: Operational Topic Without Foundation

**Query:** "How do I create a Data Unit?"

**Prerequisite check:** Tier 2 concept requires Tier 0-1

**Current knowledge assumed:** User knows "Data Unit" exists (mentioned in query)

**Prerequisite gaps likely:** May not understand Workflow Profile, Scenario Type

**Expansion strategy:**
1. Brief definition: Data Unit = Workflow Profile + Scenario + Time
2. Prerequisite: Workflow Profile (what defines scope)
3. Prerequisite: Scenario Type (affects behavior)
4. Actual query: How to create
5. Context: Why Data Units matter (consolidation scope)

---

### Example 3: Calculation Without Understanding Storage

**Query:** "Why isn't my Member Formula calculating?"

**Prerequisite check:** Tier 2 (Member Formula) requires Tier 0-1 (Member, Dynamic vs Stored)

**Likely gap:** User may not understand Dynamic vs Stored property

**Expansion strategy:**
1. Dynamic vs Stored distinction (common cause)
2. Consolidation sequence (when Member Formulas execute)
3. Member Formula syntax (correctness)
4. Troubleshooting steps

---

## Progressive Disclosure Strategy

### Level 1: Basic Definition (Always Include)
- What it is
- Where it fits in architecture
- Why it exists

### Level 2: Prerequisites (Include if gaps detected)
- What must be understood first
- Minimum knowledge required
- Related concepts

### Level 3: Operational Details (Primary content)
- How to use
- Configuration steps
- Best practices

### Level 4: Advanced Context (Include if relevant)
- Edge cases
- Integration with advanced features
- Performance considerations

### Level 5: Expert Details (Include only if requested)
- Complex scenarios
- Custom code
- Architectural implications

---

## Retrieval Rules for Prerequisites

### Rule 1: Tier Gap Check
**If query is Tier N and user context suggests Tier < N-1:**
→ Include Tier N-1 prerequisites automatically

### Rule 2: Expert Topic Warning
**If query is Tier 5:**
→ Always include "this is advanced" warning + prerequisite summary

### Rule 3: Role-Appropriate Path
**If user role known:**
→ Filter prerequisites to role-relevant path only

### Rule 4: Just-In-Time Learning
**If advanced topic detected:**
→ Provide "Start Here" link to prerequisite chain

### Rule 5: No Assumption of Knowledge
**If prerequisite terms appear in query:**
→ Brief definition included (they may have heard term but not understand)

---

## Validation Checklist

Before returning results for advanced topics:

- ✓ Identified tier level of query
- ✓ Checked for prerequisite gaps
- ✓ Included prerequisite concepts if gap detected
- ✓ Provided learning path guidance for Tier 5 topics
- ✓ Used progressive disclosure (basics → advanced)
- ✓ Avoided assuming prior knowledge

---

**Prerequisites prevent the "I don't understand the documentation" problem.**
