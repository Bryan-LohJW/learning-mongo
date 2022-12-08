# CRUD Operations - Insert and Find

## Inserting documents

There are two methods to insert documents into MongoDB

 - insertOne()

 - insertMany()

### insertOne()
```sh
db.<collection>.insertOne( {<document contents>} )
```
MongoDB automatically creates collections if it doesn't exists

All _id fields need to be filled, or it will be automatically generated

```sh
db.grades.insertOne({
  student_id: 654321,
  products: [
    {
      type: "exam",
      score: 90,
    },
    {
      type: "homework",
      score: 59,
    },
    {
      type: "quiz",
      score: 75,
    },
    {
      type: "homework",
      score: 88,
    },
  ],
  class_id: 550,
})
```

### insertMany()

```sh
db.<collection>.insertMany( <array of collections> )
```

```sh
db.grades.insertMany([
  {
    student_id: 546789,
    products: [
      {
        type: "quiz",
        score: 50,
      },
      {
        type: "homework",
        score: 70,
      },
      {
        type: "quiz",
        score: 66,
      },
      {
        type: "exam",
        score: 70,
      },
    ],
    class_id: 551,
  },
  {
    student_id: 777777,
    products: [
      {
        type: "exam",
        score: 83,
      },
      {
        type: "quiz",
        score: 59,
      },
      {
        type: "quiz",
        score: 72,
      },
      {
        type: "quiz",
        score: 67,
      },
    ],
    class_id: 550,
  },
  {
    student_id: 223344,
    products: [
      {
        type: "exam",
        score: 45,
      },
      {
        type: "homework",
        score: 39,
      },
      {
        type: "quiz",
        score: 40,
      },
      {
        type: "homework",
        score: 88,
      },
    ],
    class_id: 551,
  },
])
 ```

## Finding Documents

Using the `find()` method on a database with `$in` operator or the `$eq` operator

```sh
db.<collection>.find()
```

For the `$eq` operator, do not have to type it out for single value searches

```sh
db.zips.find({state: "AZ"})

db.zips.find({city: {$in:["PHOENIX","CHICAGO"]}})
```

Comparison operators

 - `$gt` greater than

 - `$lt` less than

 - `$lte` less than or equals to

 - `$gte` greater than or equals to

> db.<collection>.find({<field> : {$gt: <value>}})

## Querying on Array Elements

Will only return documents that have the query value within an array, not a single element

```sh
db.<collection>.find({"<field>": {$elemMatch: {$eq:<value>}}})

db.<collection>.find({"<field>": {$elemMatch: {<query1>,<query2>,...}}})
```

![Screenshot of code](Resources\04-01.png)

## Logical operators

 - $and

 - $or

And operator is implicitly within the queries

```sh
find.<collection>.find(<expression1>,<expression2>)
```

Or operator

```sh
find.<collection>.find({$or: [<expression1>,<expression2>]})
```

![Screenshot of code](Resources\04-02.png)