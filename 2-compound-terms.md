# Compound Terms & Atomic Concepts

**Purpose:** Define technical terms that MUST be treated as atomic units and should never be split during source lookup.

**Critical Rule:** These terms have specific meanings when together. Splitting them causes concept confusion.

---

## Core Compound Terms

### Cube-Related Terms

#### Cube View
**Atomic because:** Represents presentation layer component, NOT related to "Cube" storage
**Do NOT confuse with:**
- Cube (storage structure)
- View (generic display concept)
- SQL View (Relational Blending)
- IC View (Intercompany Dimension member type)

**Retrieval rule:** When query contains "Cube View", EXCLUDE general "Cube" documentation unless explicitly comparing layers.

#### Cube Reference
**Atomic because:** Specific metadata pointing to Cube, not a reference about Cubes
**Do NOT confuse with:**
- Cube (the storage structure itself)
- Cross-cube references (calculation concept)

---

### Workflow-Related Terms

#### Workflow Profile
**Atomic because:** Specific configuration object defining Data Unit scope
**Do NOT confuse with:**
- Profile (generic concept)
- Time Profile (calendar configuration)
- User Profile (security concept)

**Retrieval rule:** "Profile" alone defaults to Workflow Profile 99% of the time.

#### Workflow Channel
**Atomic because:** Controls timing and sequencing, not a channel related to workflow
**Do NOT confuse with:**
- Workflow (general process)
- Channel (communication concept)

#### Parent Workflow Profile / Child Workflow Profile
**Atomic because:** Hierarchical relationship terminology
**Do NOT confuse with:** Generic parent/child relationships

---

### Calculation-Related Terms

#### Member Formula
**Atomic because:** Specific calculation type attached to Dimension Members
**Do NOT confuse with:**
- Formula (generic calculation)
- Business Rule (different calculation mechanism)
- Complex Expression (formula syntax)

**Retrieval rule:** "Formula" queries should check context for "member" or "account" to disambiguate.

#### Business Rule
**Atomic because:** Specific VB.NET-based calculation component
**Do NOT confuse with:**
- Rule (generic concept)
- Transformation Rule (ETL concept)
- Confirmation Rule (validation concept)
- Member Formula (different calculation type)

**Retrieval rule:** "Rule" in calculation context defaults to Business Rule.

#### Consolidation Process
**Atomic because:** The execution engine for calculations
**Do NOT confuse with:**
- Consolidation Members (metadata)
- Consolidation Dimension (structure)
- Consolidation (generic term)

#### Consolidation Members
**Atomic because:** Specific member types (Top, Share, Elimination)
**Do NOT confuse with:**
- Consolidation Process
- Members (generic)

---

### Data Management Terms

#### Data Source
**Atomic because:** Configuration for external data connection
**Do NOT confuse with:**
- Source (generic)
- Data (generic)

#### Data Management
**Atomic because:** Specific OneStream subsystem for ETL
**Do NOT confuse with:**
- Data management (generic concept)
- Management (generic)

#### Transformation Rule
**Atomic because:** ETL-specific data modification rule
**Do NOT confuse with:**
- Business Rule (calculation)
- Confirmation Rule (validation)
- Rule (generic)

#### Stage Engine
**Atomic because:** Specific pre-load validation engine
**Do NOT confuse with:**
- Stage (generic concept)
- Engine (generic)

#### Finance Engine
**Atomic because:** Post-load calculation engine
**Do NOT confuse with:**
- Stage Engine (different engine)
- Consolidation (calculation type)

---

### Dimension-Related Terms

#### Dimension Member
**Atomic because:** Specific metadata element within Dimension
**Do NOT confuse with:**
- Dimension (the structure)
- Member (generic concept)

#### User Defined Dimensions (UD1-UD8)
**Atomic because:** Specific 8 dimensions for custom usage
**Do NOT confuse with:**
- User Defined (generic custom concept)
- Dimension (generic)

#### Extensible Dimensionality
**Atomic because:** Feature allowing Entity/UD expansion
**Do NOT confuse with:**
- Extensibility (generic)
- Dimension (generic)

---

### Presentation-Related Terms

#### Member Filter
**Atomic because:** Cube View component for data selection
**Do NOT confuse with:**
- Filter (generic)
- Member (generic)

#### Form Template
**Atomic because:** Data entry form configuration
**Do NOT confuse with:**
- Template (generic)
- Form (generic)

#### Form Child Profile
**Atomic because:** Sub-form configuration
**Do NOT confuse with:**
- Child (generic relationship)
- Profile (Workflow Profile)

#### Point of View (POV)
**Atomic because:** Specific Cube View selection mechanism
**Do NOT confuse with:** View (generic concept)

---

### Security-Related Terms

#### Security Group
**Atomic because:** OneStream security object
**Do NOT confuse with:**
- Group (generic)
- Security (generic concept)

#### Cube Access
**Atomic because:** Specific permission type for Cube data
**Do NOT confuse with:**
- Access (generic)
- Cube (storage)

#### Relationship Security
**Atomic because:** Security based on dimensional relationships
**Do NOT confuse with:**
- Security (generic)
- Relationship (generic)

---

### Design Pattern Terms

#### Standard Cube
**Atomic because:** Specific Cube design pattern
**Do NOT confuse with:**
- Cube (generic)
- Standard (generic term)

#### Standard Large Sparse
**Atomic because:** Specific Cube design for sparse data > 750k cells
**Do NOT confuse with:**
- Standard Cube
- Large (size reference)
- Sparse (data characteristic)

#### Hybrid Cube
**Atomic because:** Specific dual-storage design pattern
**Do NOT confuse with:**
- Hybrid (generic)
- Cube (generic)

#### BI-Blend
**Atomic because:** Specific aggregation design pattern
**Do NOT confuse with:**
- BI (business intelligence generic)
- Blend (generic mixing)
- Relational Blending (different feature)

#### Relational Blending
**Atomic because:** Specific SQL pass-through feature
**Do NOT confuse with:**
- BI-Blend
- Relational (generic database term)
- SQL View

---

### Workflow State Terms

#### Data Unit
**Atomic because:** Specific calculation scope unit
**Do NOT confuse with:**
- Data (generic)
- Unit (generic)
- Data Cell (intersection value)
- Data Buffer (in-memory storage)

**Retrieval rule:** Extremely important - Data Unit (scope) ≠ Data Cell (value)

#### Scenario Type
**Atomic because:** Metadata defining planning/actual/forecast
**Do NOT confuse with:**
- Scenario (generic situation)
- Type (generic classification)

---

### API Terms

#### BRApi
**Atomic because:** Business Rule API for calculations
**Do NOT confuse with:**
- API (generic application interface)
- Business Rule (the component that uses BRApi)

---

### Translation Terms

#### FX Rate
**Atomic because:** Foreign Exchange rate table
**Do NOT confuse with:**
- Rate (generic)
- Translation (generic language conversion)

---

## Complete Atomic Term List (45+)

For quick reference during retrieval:

1. Cube View
2. Cube Reference
3. Workflow Profile
4. Time Profile
5. Workflow Channel
6. Parent Workflow Profile
7. Child Workflow Profile
8. Member Formula
9. Business Rule
10. Consolidation Process
11. Consolidation Members
12. Consolidation Dimension
13. Data Source
14. Data Management
15. Transformation Rule
16. Confirmation Rule
17. Stage Engine
18. Finance Engine
19. Dimension Member
20. User Defined Dimensions (UD1-UD8)
21. Extensible Dimensionality
22. Member Filter
23. Form Template
24. Form Child Profile
25. Point of View (POV)
26. Security Group
27. Cube Access
28. Relationship Security
29. Standard Cube
30. Standard Large Sparse
31. Hybrid Cube
32. BI-Blend
33. Relational Blending
34. Data Unit
35. Data Cell
36. Data Buffer
37. Scenario Type
38. BRApi
39. FX Rate
40. Extensible Document
41. Complex Expression
42. Event Handler
43. Named Business Rule
44. Excel Add-in
45. Cube Design Pattern

---

## Retrieval Application Rules

### When Processing Queries:

1. **Scan for compound terms** using the list above
2. **Treat as atomic** - do not split during concept matching
3. **Apply "Do NOT confuse with" rules** to exclude irrelevant results
4. **Check context signals** if term has multiple meanings
5. **Default to most common** interpretation if ambiguous

### Embedded Compound Terms in API Identifiers

If an exact identifier contains an atomic term, preserve both the full identifier and the embedded concept.

**Example:** `FdxExecuteCubeView`
- Full identifier: exact API lookup target
- Embedded atomic term: `Cube View`
- Do NOT split into generic tokens such as `cube`, `view`, or `execute`

**Retrieval rule:**
- Exact-match the full identifier in API docs first
- Retrieve concept docs for the embedded atomic term second
- Use owner type, signature, and nearby APIs to interpret purpose
- Exclude generic token matches unless exact identifier search is exhausted

### Example Application:

**Query:** "How do I create a Cube View?"

**Compound term detected:** "Cube View" (atomic)

**Apply exclusion rule:**
- EXCLUDE: General "Cube" documentation
- EXCLUDE: "View" generic concepts
- EXCLUDE: "SQL View" documentation

**Include only:**
- Cube View-specific documentation
- Prerequisites (Cube basics, Dimension Members)
- Common components (Member Filters, Parameters)

---

## Validation Check

Before returning retrieval results, verify:

- ✓ No compound terms were split
- ✓ "Do NOT confuse with" exclusions applied
- ✓ Context-appropriate interpretation selected
- ✓ Related atomic terms included if co-occurrence rule exists

---

**This module prevents a common OneStream failure mode: splitting atomic technical terms.**
