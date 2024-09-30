### **Fourth Normal Form (4NF)**

#### **Definition:**
A relation is in **4NF** if it is already in **Boyce-Codd Normal Form (BCNF)** and does not have any **multi-valued dependencies**.

#### **Multi-valued Dependency (MVD):**
An MVD occurs when for a certain attribute in a table, you can have multiple values for another attribute, independent of any third attribute. In simpler terms, an MVD occurs when one attribute determines multiple independent values of another attribute, without depending on other attributes in the relation.

#### **Violation of 4NF:**
When a relation contains non-trivial multi-valued dependencies, it violates 4NF.

#### **Example:**
Let’s consider a table **Student_Subject_Hobby** that records a student’s subject of study and their hobbies.

| Student | Subject   | Hobby    |
|---------|-----------|----------|
| John    | Math      | Painting |
| John    | Math      | Football |
| John    | Physics   | Painting |
| John    | Physics   | Football |

- Here, **Student** is dependent on both **Subject** and **Hobby**. 
- John can study multiple subjects (Math and Physics), and he can also have multiple hobbies (Painting and Football), independent of the subjects.
  
The above table has a **multi-valued dependency**:
- Student →→ Subject
- Student →→ Hobby

The two MVDs are independent of each other. This redundancy is unnecessary, and the relation can be split into two tables to remove the MVD.

#### **To Bring in 4NF:**
We decompose the table into two:

**Table 1: Student_Subject**

| Student | Subject   |
|---------|-----------|
| John    | Math      |
| John    | Physics   |

**Table 2: Student_Hobby**

| Student | Hobby    |
|---------|----------|
| John    | Painting |
| John    | Football |

By splitting the table, we remove the MVD and achieve 4NF.

---

### **Fifth Normal Form (5NF)**

#### **Definition:**
A relation is in **5NF** (or Project-Join Normal Form, PJNF) if it is already in **4NF** and cannot be decomposed into smaller relations without losing information (i.e., no **join dependency** exists).

#### **Join Dependency (JD):**
A **join dependency** occurs when a table can be split into multiple tables and then recombined (joined) to get back the original table. If this is possible without loss of data, then the original table is not in 5NF.

#### **Example:**
Consider a table **Supplier_Parts_Project** that records the parts supplied by a supplier for a project.

| Supplier | Part  | Project  |
|----------|-------|----------|
| S1       | P1    | Pr1      |
| S1       | P2    | Pr1      |
| S2       | P1    | Pr2      |
| S2       | P2    | Pr2      |

This table indicates:
- Supplier S1 supplies parts P1 and P2 for Project Pr1.
- Supplier S2 supplies parts P1 and P2 for Project Pr2.

However, there may be an implicit assumption that:
- Supplier S1 can supply **any part** for Project Pr1.
- Supplier S2 can supply **any part** for Project Pr2.

This can result in multiple join dependencies. 

#### **Violation of 5NF:**
If the data can be divided and then re-joined without loss of information, it violates 5NF.

#### **To Bring in 5NF:**
We decompose the relation into three tables:

**Table 1: Supplier_Project**

| Supplier | Project  |
|----------|----------|
| S1       | Pr1      |
| S2       | Pr2      |

**Table 2: Supplier_Part**

| Supplier | Part  |
|----------|-------|
| S1       | P1    |
| S1       | P2    |
| S2       | P1    |
| S2       | P2    |

**Table 3: Part_Project**

| Part  | Project  |
|-------|----------|
| P1    | Pr1      |
| P2    | Pr1      |
| P1    | Pr2      |
| P2    | Pr2      |

This decomposition satisfies 5NF since no further meaningful decomposition can be made, and we can still recover the original relation by joining these three tables.

---

### **Summary:**
- **4NF** handles multi-valued dependencies by breaking the table into smaller relations, where each attribute depends only on the key.
- **5NF** ensures that a table cannot be decomposed further based on join dependencies, preserving all relationships without data loss.

Both normal forms aim to reduce redundancy and anomalies in the database.
