http://guide.meteor.com/collections.html#default-value

# Meteor Collections
----

Source: [http://guide.meteor.com/collections.html#default-value]

One thing that the Collection2 package does is [“clean” the data](https://github.com/aldeed/meteor-simple-schema#cleaning-data) before sending it to the database. This includes but is not limited to:

1. Coercing types - converting strings to numbers
2. Removing attributes not in the schema
3. Assigning default values based on the `defaultValue` in the schema definition


However, sometimes it’s useful to do more complex initialization to documents before inserting them into collections. For instance, in the Todos app, we want to set the name of new lists to be `List X` where `X` is the next available unique letter.

To do so, we can subclass `Mongo.Collection` and write our own `insert()` method:

```javascript
class ListsCollection extends Mongo.Collection {
  insert(list, callback) {
    if (!list.name) {
      let nextLetter = 'A';
      list.name = `List ${nextLetter}`;

      while (!!this.findOne({name: list.name})) {
        // not going to be too smart here, can go past Z
        nextLetter = String.fromCharCode(nextLetter.charCodeAt(0) + 1);
        list.name = `List ${nextLetter}`;
      }
    }

    // Call the original `insert` method, which will validate
    // against the schema
    return super.insert(list, callback);
  }
}

Lists = new ListsCollection('Lists');
```
