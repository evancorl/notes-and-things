Index Types
----

**Single Field Indexes**: Only includes data from
a signle field of the document in a collection. MongoDB supports single
field indexes on field at the top level of a document _and_ on fields in
sub-documents.
**Compound Indexes**: Includes more than one field of the documents in a collection.
** Multikey Indexes**: An index on an array field, adding an index key for
each value in the array.
** Geospatical Indexes and Queries**: Support location-based searches on data that is stored as either GeoJSON objects or legacy coordinate pairs. 
** Text Indexes**: Support search of string content in documents.
** Hashed Index**: Maintain entries with hashes of the values of the indexed field and are primarily used withsharded clusters to support hashed shard keys.
