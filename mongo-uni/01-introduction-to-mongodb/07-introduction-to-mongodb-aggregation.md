# Aggregation

## What is aggregation?

Aggregation is an analysis and summary of data.

Stage is an aggregation operation performed on the data.

Aggregation pipeline is a series of stages completed one at a time in order.

In the different stages, data can be filtered, sorted, grouped, and transformed.

Aggregation can be done in Atlas, but in this lesson it is done in CLI

```sh
db.collection.aggregate([
    {$stage_name: {<expression>}},
    {$stage_name: {<expression>}},
])
```

## Stages

`$match` 

 - filters for data that matches criteria

 - use it as early as possible in pipeline to use indexes, and reduce number of documents and reduce processing time

```sh
db.zip.aggregate([
    {$match: {"state": "CA"}}
])
```

`$group` 

 - groups documents based on criteria

 - Groups documents by a group key

 - Output is one document for each unique value of the group key

```sh
{
    $group:{
        _id:<expression>, # Group key
        <field>: {<accumulator> : <expression>}
    }
}

{
    $group:{
        _id: "city", # Group key
        totalZips: {$count : {}}
    }
}
```

`$sort` 

 - puts the documents in a specified order

```sh
{
    $sort: {
        pop: -1
    }
}
```

`$limit` 

 - limits the number of documents that are passed on to the next aggregation stage

```sh
{
    $limit: 3
}
```

`$project` 

 - determines output shape, specify existing or new fields in the document

 - similar to find operation

 - should be last stage to format output

 - can specify new values for new fields, or new values for existing fields

```sh
{
    $project: {
        <field>: <value>,
        <field>: <value>,
        ...
        <field>: <new value>
    }
}
```

`$set` 

 - adds or modifies fields in the pipeline

 - useful when want to change existing fields in ipeline or add new ones to be used in upcoming pipeline stages

```sh
{
    $set : {
        pop_2022: {$round: {$multiply: [1.003, "$pop"]}}
    }
}
```

`$count`

- count documents in the pipeline

```sh
{
    $count:<field_name>
}
```

`$out`

 - writes the documents that are returned by an aggregation pipeline into a collection

 - must be the last stage

 - creates a new collection if it does not already exist

 - if collection exists, `$out` replaces the existing collection with new data

```sh
{ # for different database
    $out: {
        db: "<db>",
        coll:"<newcollection>"
    }
}

{ # for same database
    $out: {
        coll: "<newcollection>"
    }
}
```

## Field references

`"$field_name"` is to put in preset values