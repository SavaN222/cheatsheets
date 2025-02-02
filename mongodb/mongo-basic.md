# mongoDB-cheatsheets
- mongod [database]
- mongosh [shell]

In the background mongo uses BSON - binary data

## basic commands + CRUD
- show dbs = list all dbs
- use <name> = switch to <name>, created if not exist
- db.products.insertOne({obj}) = insert to current DB <name>, products is the name of the collection[table]
- db.products.find() - return all obj, .pretty() for prettier output
  
### Create
- insertOne, insertMany
  - (data, options)

### Read
- find, findOne = returns first
  - (filter, options)

**find does not** return all data, it returns cursor similar like pagination, `find().toArray()` will return all.


### Update
- updateOne, updateMany
  - (filter, data, options )
- replaceOne = delete + insert
Example: 
```mongodb
db.collection.updateOne(
    {distance: 12000},
    {$set {
        market: 'delete'
    }}
)
```
```mongodb
db.collection.updateMany(
    {},
    {$set {
        market: 'delete'
    }}
)
```

**UPDATE** .update() will override whole object if `$set` is not specified while updateOne and updateMany will throw error if `$set` is not specified, is similiar like `replaceOne`, but is better to use `replaceOne`
**same for delete**

### Delete
- deleteOne, deleteMany
  - (filter. options)

### params
- $gt = greatherThan
```mongodb
db.collection.find(
    {distance:
        {$gt: 1000}
    }
)
```

### other functions
.find().forEach()

# Projection
**Mongo data**
```json
id: "ObjectID('randomHash'),
name: "John"
lastname: "Doe"
...more fields
```
**Projectiom trim data**
```json
name: "John"
lastname: "Doe"
```
.find({}, {name: 1}) // 1st arg means WHERE, 2nd what to retrieve but id will be included, {_id: 0} means not include id which is included by default

**Projections are fast since they are happening on mongoDB server**

