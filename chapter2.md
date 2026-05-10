# Data Models and Query Languages

Applications are built by layering one data model on top of another. For each layer the key question is: *how is it represented in terms of the next-lower layer?*

## Relational Model vs Document Model

**Relational model (SQL)**: Data is organized into relations (tables), where each relation is an unordered collection of tuples (rows)

### NoSQL

Driving forces behind adoption:
* Greater scalability
* Free and open-source
* Specialized query operations
* Combat the restrictiveness of relational schemas
* More expressive and dynamic

### The Object-Relational Mismactch

**impedance mismatch**: translation layer is required between object-oriented programming languages and table-oriented SQL data models.
* These translation layers are called **object-relational mapping (ORM)** framerworks

Problems occur in SQL data model with one-to-many mappings
* **JSON** reduces the impedenance mismatch by having better *locality*, meaning all relevant information is in one place
* We can have SQL rows contain a JSON-encoded column, but in this case we cannot use the database to query for values inside the encoded column
* The alternative is to have SQL columns pointing to other columns, but in this case we need multiple nested queries

### Many-To-One and Many-To-Many Relationships

Sometimes we store data as ID mappings, not plain text
* *When you use an ID*, the information meaningful to humans is tored in one place, and things that refer to it use the ID
* *When you use plain text*, you are duplicating the human-meaningful information in every record that uses it

**Advantage of using IDs**
Because it has no meaning to humans, it never has to change. This allows:
* The meaning behind it to change
* Easy joins in the database by using ID
* IDs can go from referencing simple text strings to entities with their own information

