# Data Modelling

- ER diagrams are usually designed by database engineers.

## Data Warehousing

- It is used for reads.
- Used for analytical queries to derive patterns.
- Data is structured.
- Denormalization does occur.

### OLAP

- OLAP is used for data warehousing.
  - It is a tool used for storing huge amounts of data in a structured form.
- OLAP can hold data for more than 5 years.

### Dimensional Modelling

There are two types of tables:

1. **Fact table**
2. **Dimension table**

#### Fact Tables

- This is where core data is stored.
- Contains business metrics that can be evaluated.
- Contains numerical data.
- Contains foreign keys from other tables.

**Examples:**

- In E-commerce: `Sales` table
- In Healthcare: `PatientVisit` table

#### Dimension Tables

- They contain descriptive information.

**Examples:**

- In E-commerce: `Product`, `Customer`

### Schema Designs

3 types:

1. **Star schema**
2. **Snowflake schema**
3. **Galaxy schema**

#### Star Schema (Just do it)

- Simple and intuitive choice.
- Only one fact table.
- Can have multiple dimension tables.
- **Advantages:**
  - Easy to understand.
  - Fast performance.
- **Disadvantages:**
  - Redundancy might exist in dimension tables.

#### Snowflake Schema (When you need more normalization)

- 1 fact table.
- Multiple dimension tables.
- More joins are involved.

#### Galaxy Schema

- Many fact tables.
- Shared dimension tables.