# CRUD Operations - Replace and Delete

## Replacing documents

`replaceOne` is done my replacing the whole document with updated data, while keeping the same `_id`. Options will not be discussed in this lesson

```sh
db.<collections>.replaceOne(<filter>,<replacement>,<options>)

db.books.replaceOne({_id:<value>}, {title:"title", ISBN:"123456": authors:["Bryan"]})
```

## Updating documents

`updateOne()` with operators `$set` and `$push` and the option `upsert()`

```sh
db.<collection>.updateOne(<filter>, <update>, <option>)
```

`$set`: adds new fields and values to a document or replaces the value of a field with a specified value

`$push`: appends a value to an array or adds the array field with the value as its element

The `updateOne()` method has other operators such as `$pop`, `$unset`, `$inc` to be used

`upsert` options will insert a document with the provided information if matching documents do not exist. `{upsert:true}`

### findAndModify

This method returns the document that has just been updated, do not require to update document and find in two separate actions

```sh
db.<collection>,findAndModify({query:<field>, update:<field>, new:true})
```

### updateMany()

Same as updateOne() but will update all documents that matches the filter document

This is not an all or nothing operation, if some matches fail, the operation would not roll back other updates. To fix this, perform the operation again

Updates will be visible as soon as they are performed

## Deleting documents

`deleteOne()` and `deleteMany()`

The both methods accept a filter document and option document.