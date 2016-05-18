# Mongo Indexes
----

Indexes support the efficient execution of queries in MongoDB. 

Collection Scan: scan every document in a collection, to select those documents that match the query statement. If an appropriate index exists for a query, MongoDB can use the index to limit the number of documents it must inspect.

### Index Types
----
* **Single Field Indexes**: Only includes data from a signal field of the document in a collection. MongoDB supports single field indexes on field at the top level of a document _and_ on fields in sub-documents.
* **Compound Indexes**: Includes more than one field of the documents in a collection.
* **Multikey Indexes**: An index on an array field, adding an index key for
each value in the array.
* **Geospatical Indexes and Queries**: Support location-based searches on data that is stored as either GeoJSON objects or legacy coordinate pairs. 
* **Text Indexes**: Support search of string content in documents.
* **Hashed Index**: Maintain entries with hashes of the values of the indexed field and are primarily used withsharded clusters to support hashed shard keys.

### Index Properties
----
* **Unique**
  * A unique index causes MongoDB to reject all documents that contain a duplicate value for the indexed field.
* **Sparse**
  * Sparse indexes only contain entries for documents that have the indexed field, even if the index field contains a null value.
  * The index skips over any document that is missing the indexed field. 

**Default *_id* Index**
  * A Unique index on the `_id` field is created during the creation of a collection.
  * This prevents clients from inserting two documents with the same value for the `_id`.
  * You cannot drop this index

### Methods
---
**Return All Indexes for a Collection**
  * `db.collection.getIndexes()`

**Create an Index**
  * `db.collection.createIndex(<key and index type specifications>, <options>)`
  * the 1 indicates an ascending sort order and -1 a descending sort order.

**List All Indexes for a Database**
```
db.getCollectionNames().forEach(function(collection) {
  indexes = db[collection].getIndexes();
  print("Indexes for " + collection + ":");
  printjson(indexes);
});
```

### Meteor Specific
----
* **Meteor Mongo**
  * Minimongo doesn't currently have indexes.
