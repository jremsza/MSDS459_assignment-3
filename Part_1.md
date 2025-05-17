# Part 1: Summary of Knowledge Graphs - Chapter 12

### SPARQL

Knowledge graphs (KGs) can be queried using structured methods like SPARQL, a W3C standard for RDF graphs, or key-value stores used in NoSQL. SPARQL, favored by the Semantic Web community, uses graph pattern-matching to query RDF data, allowing variable bindings and operations like joins, unions, and projections. A basic SPARQL query involves triple patterns with variables, literals, or IRIs to match and retrieve data, though it may need extensions like SQL features for more complex real-world queries.

**Query Language**<br>
key components of a SPARQL query:<br>
PREFIX defines shorthand for URL namespaces<br>
SELECT specifies the variables to return (similar to SQL queries)<br>
FROM indicates the dataset to query(similar to SQL queries)<br>
WHERE sets conditions using graph patterns (e.g., matching entities of type foaf:Person with a homepage)<br>
ORDER BY sorts the results (e.g., by homepage in descending order)

- **Subqueries**
Subqueries in SPARQL is a technique that allows to nest one query inside another, enabling more complex data retrieval from RDF graphs. They work like subqueries in SQL, letting you break down a problem into smaller parts. A subquery is enclosed in curly braces {} within the main query's WHERE clause, and its results can be used by the outer query.

A further look into using SPARQL as a tool gave a hit on popoular libries that enable it to be used in a Python envirnorment: SPARQLWrapper, RDFlib.
https://sparql.dev/article/Top_10_SPARQL_libraries_for_Python_developers.html


### Realational processing of queries of knowledge graphs
SPARQL queries on knowledge graphs (KGs) can leverage decades of SQL query optimization, despite RDF and KGs not being directly representable as tables. Relational database management systems (RDBMSs) efficiently handle large datasets with indexing, and relational RDF stores have been developed to combine KG benefits with RDBMS query execution speed. These stores are categorized into three types: triple (vertical) table stores, which store RDF triples in a three-column table (subject, predicate, object); property (n-ary) table stores, modeling multiple RDF properties as n-ary table columns for the same subject; and horizontal table stores, organizing RDF triples into one horizontal table or sets of vertically partitioned binary tables per property.

- **Triple Verticle Scores**<br>
A method to store RDF data in RDBMS using a single three-column table (subject, predicate, object) with indexes on each column for faster joins. While simple for basic queries, scalability becomes an issue as the dataset grows due to slow self-joins on the large table for complex SPARQL queries. Examples like 3store use a central triple table with hashes and a symbols table for lookups, while RDF-3X and Hexastore optimize performance with extensive indexing. 

- **Propertry Table Stores**<br>
Propsed as an alternative to triplestores for RDF data in RDBMS, aiming to reduce self-joins by grouping multiple triple patterns for the same subject into a single table with columns for fixed properties. Jena, an early example, used a statement table for triples and separate tables for literals and resources, but required multiple joins. Jena2 improved this with denormalized schemas, encoding value types and using a literals table for large values, though at the cost of more space. 

- **Horizontal Stores**<br>
With this approach the triples table is split into n two-column tables (one per unique property in the RDF graph), with each table holding subjects and objects for that property, sorted by subject for fast merge joins. It reduces union clauses by grouping data by property, but struggles with sparse datasets, leading some to suggest a single table with interpreted storage. Extensions like roStore improve this by organizing tables by property hierarchies, reducing table counts in domains like biology.

### NoSQL

There are limitations with triplestores and SPARQL, especially with noisy or schema-less datasets, as RDF isn’t always ideal compared to normalized relational databases. NoSQL databases, are an alternitive that offer flexible, schema-less storage and querying, avoiding the rigid constraints of RDBMS. NoSQL gained traction for handling unstructured data, as seen in systems like Amazon and Google, and is now widely used for web and Big Data applications. While RDBMS provide robust features (ACID properties), they don’t scale well for all use cases, adaptable choice despite lacking some RDBMS guarantees.

- **JSON**: Java Script Object Notation - A data format used in NoSQL key-value stores for easy human and machine readability. JSON is built on two structures: a collection of name/value pairs (like objects or dictionaries in programming languages, e.g., {"name": "A. Einstein", "age": 29}) and an ordered list of values (like arrays, e.g., ["A. J. Bose", "M. Kejriwal"]). Keys and values commonly use integers and strings, but values can also be nested JSON objects or arrays, enabling recursive data structures.

- **Key-Value Stores**: A simple database that uses an array as the data model that is made up of each key is associated with one and only one value, known as a key-value pair. This value is stored as a blob with no up front schema required. Generally the key-value store have no query langauge but instead use the GET, PUT, DELETE commands for retreival or updates. Two examples of json/key-value stores are MongoDDB and Elasticsearch

    - MongoDB: Supports a schema free document store build on Apache Lucene
    - Elasticsearch: A distributed RESTful search and analytics engine that promotes itself with robust search capabilites

https://www.mongodb.com/docs/guides/

https://www.elastic.co/elasticsearch/features


- **Graph Database**: Loosley defined as models where data structures for the schema and instances are modeled as graphs and data manipulation is expressed by graph-orientated operations and type constructors. Although KGs are a major application, graph databases serve many graph-theoretic applications, particularly where data interconnectivity is as important as the data itself.
Key advantages of graph databases include:<br>
More natural modeling of structured but non-tabular data<br>
Ability to store entity information in nodes while representing relationships as edges<br>
Leveraging existing graph querying languages (like SPARQL) and algorithms<br>
Providing high-level abstraction for queries through specialized query languages

- Neo4j: An open-source, NoSQL native graph database offering for-profit enterprise needs with open-source community development.<br>
Neo4j uses the "property graph" model with three core components:

- Nodes: Entities that can hold attributes (key-value pairs called properties) and can be tagged with labels to indicate their roles or attach metadata<br>
- Relationships: Directed, named connections between nodes that always have direction and type
Properties: Data stored on both nodes and relationships

- Relationships in Neo4j can have their own properties (unlike in traditional RDF settings), making features like reification easier and more seamless.
In practice, relationships often have quantitative properties such as weights, costs, and ratings.

Neo4j uses cypher as the query language similar to SQL that is designed to be human readable 

https://neo4j.com/docs/
https://neo4j.com/videos/neo4j-live-how-to-build-a-knowledge-graph/

### References

Elastic.co. 2022. “Elasticsearch Features List.” March 10, 2022. https://www.elastic.co/elasticsearch/features.

MongoDB.com. 2022. “MongoDB Documentation: Guides.” June 27, 2022. https://www.mongodb.com/docs/guides/.

Neo4j.com. 2024. “Neo4j Documentation.” May 9, 2024. https://neo4j.com/docs/.

Neo4j.com. 2025. “Neo4j Live: How to Build a Knowledge Graph.” April 22, 2025. https://neo4j.com/videos/neo4j-live-how-to-build-a-knowledge-graph/.

Kejriwal, Mayank, Craig A. Knoblock, and Pedro Szekely. 2021. Knowledge Graphs: Fundamentals, Techniques, and Applications. Cambridge, MA: MIT Press. [ISBN-13: 978-0262045094] Chapter 12 Structured Querying, pages 307–335.

Sparql.dev. 2025. “Top 10 SPARQL Libraries for Python Developers.” May 17, 2025. https://sparql.dev/article/Top_10_SPARQL_libraries_for_Python_developers.html.