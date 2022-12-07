# CRUD Operations - Modifying Query Results

## Limit and order query

`cursor.sort()` and `cursor.limit()`

Cursor is a pointer to the result set of a query, the `find()` method returns a cursor and points to the documents that points to the documents that match that query

Cursor methods are chained to queries to perform actions on the result set before returning the data to the client

```sh
db.<collection>.find(<query>).sort({<field> : 1}) # 1 is asc, -1 is desc
```

For sorting, capital and lowercase letters are sorted separately, but can be changed by using an option

```sh
db.<collection>.find(<query>).sort({<field> : 1}).limit(3) 
```

## Projections

Shows only the fields specified to leave out unnecessary information, able to improve bandwidth performance by choosing which fields to return.

This can be done by putting the projection argument as the second parameter in the find method.

Inclusions and exclusions cannot be combined, except for _id

```sh
db.companies.find({query:value},{field:1,field:1}).sort()

db.inspections.find({sector:"Restaurant - 18"}, {business_name:1.result:1,_id:0})

# 1 is to include, 0 is to exclude
```

## Document Count

```sh
db.<collection>.countDocuments(<query>,<options>)
```