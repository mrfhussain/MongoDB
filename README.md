# MongoDB
Everything to do with MongoDB

## Indexing in MongoDB
Indexes in MongoDB are special data structures that store a small portion of the collection’s data set in an easy-to-traverse form. They are crucial for improving the efficiency of query operations. Without indexes, MongoDB must scan every document in a collection to return query results, which can be very slow for large datasets.

### Key Concepts
1. **Single Field Index:** Indexes a single field of a document. This is the most basic type of index.
JavaScript
`db.collection.createIndex({ field: 1 })`
2. **Compound Index:** Indexes multiple fields within a document. Useful for queries that sort or filter on multiple fields.
JavaScript
`db.collection.createIndex({ field1: 1, field2: -1 })`
3. **Multikey Index:** Indexes array fields. Each value in the array is indexed separately.
JavaScript:
`db.collection.createIndex({ arrayField: 1 })`
4. **Text Index:** Supports text search queries on string content.
JavaScript:
`db.collection.createIndex({ field: "text" })`
5. **Geospatial Index**: Supports queries for geospatial data.
JavaScript:
`db.collection.createIndex({ location: "2dsphere" })`

### Creating an Index
1. To **create an index**, use the createIndex method:
JavaScript:
`db.collection.createIndex({ field: 1 })`
This command creates an ascending index on the specified field.
2. **Dropping an Index**
To drop an index, use the dropIndex method:
JavaScript:
`db.collection.dropIndex({ field: 1 })`
3. **Viewing Indexes**
To view all indexes on a collection, use the getIndexes method:
JavaScript
`db.collection.getIndexes()`

### Performance Considerations
**Read Performance:** Indexes improve the speed of read operations by allowing MongoDB to quickly locate the data.
**Write Performance:** Indexes can slow down write operations because MongoDB must update the indexes whenever a document is inserted, updated, or deleted.
### Use Cases
**Frequent Queries:** If your application frequently queries certain fields, creating indexes on those fields can significantly improve performance.
**Sorting:** Indexes can also improve the performance of sort operations.
For more detailed information, you can refer to the MongoDB Manual on Indexes (https://www.mongodb.com/docs/manual/indexes/) or the GeeksforGeeks article on Indexing in MongoDB (https://www.geeksforgeeks.org/indexing-in-mongodb/)

### Statistics for Indexing
**Ref:** https://www.youtube.com/watch?v=D14wWW9EEx8
#### Execution statistics
**Using `$indexStats`**

The `$indexStats` aggregation stage returns statistics regarding the use of each index for a collection. Here’s an example of how to use it:
```
db.collection.aggregate([
  { $indexStats: {} }
])
```
This command will provide details on how often each index is used, which can help you understand the performance and usage of your indexes (https://www.mongodb.com/docs/manual/tutorial/measure-index-use/).
**Using `explain`**

The explain method provides detailed execution statistics about the query process, including the index used, the number of documents scanned, and the time taken to process the query. You can use it in executionStats mode to get these details:
```
db.collection.explain("executionStats").find({ field: "value" })
```
Or, you can append the explain method to a query:
```
db.collection.find({ field: "value" }).explain("executionStats")
```
This will return a detailed report on the query execution, including which indexes were used and how efficient they were (https://www.mongodb.com/docs/manual/tutorial/measure-index-use/) (https://www.mongodb.com/docs/manual/reference/explain-results/)
