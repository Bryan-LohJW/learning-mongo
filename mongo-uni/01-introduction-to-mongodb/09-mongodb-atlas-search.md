# Atlas Search

## Relevance-Based Search

This type of search surface records based on a search term, it is not a database search

MongoDB uses Apache Lucene search engine for its database search functions

## Search Indexes

Used to specify how the algorithm should work with a set of data

Specifies how records are referenced for relevance-based search

Configurations

 - Index Analyzer

 - Search Analyzer

 - Dynamic Mapping

 - Store Full Document

 = Field Mappings

Dynamic mapping

## Searching with Dynamic Index

 - All fields will be indexed except booleans, objectIds, and timestamps

After creating a search index, a query can be made and each result will have a score depending on how prevalent the term is in any of the record. The higher the score the higher it is on the list. The scores can be changed by assigning different weights to the fields

## Searching with Static Index

More specific in terms of the fields to search for. The fields to search are always the same. This makes the search quicker than dynamic search

To make a static search, toggle off dynamic search and add field that users might query. Select the field data type

Fields that are not indexed will not will searched

## $search and $compound

Creating aggregation pipeline with search stage, and include compound operator.

Within the `$search` stage, can include options for highlighting, count, etc but will not be going through in this lesson

`$compound` operator is nested in the search stage

 - must (only include results that match the clause)

 - must not (don't include results that match the clause)

 - should (assign weight to record that match the clause)

 - filter (remove results that do not match the clause, but will not affect the score)

```sh
$search {
  "compound": {
    "must": [{
      "text": {
        "query": "field",
        "path": "habitat"
      }
    }],
    "should": [{
      "range": {
        "gte": 45,
        "path": "wingspan_cm",
        "score": {"constant": {"value": 5}}
      }
    }]
  }
}

{
    "compound": {
      "filter": [{
        "text": {
          "query": "Online",
          "path": "purchaseMethod"
        }
      }],
      "should": [{
        "text": {
          "query": "notepad",
          "path": "items",
          "score": {"constant": {"value": 5}}
        }
      }]
    }
  }
```

## Group Search Results by Using Facets

Facets are buckets that we group our search results into, like categories. Data types can be used for grouping, can use numbers, dates, and strings.

First create field mappings for the field that will be used to create groupings. Make sure dynamic mapping is toggled off. The datatype should be `<datatype>facet`

Also add the fields that will be used for quering in the field mapping

Use the searchMeta stage in aggregation to see the facets and the count of data in each facet.

```sh
{
    "facet": {
        "operator": {
            "text": {
                "query": ["Nothern Cardinal"],
                "path": "species_common"
                }
            }
        },
        {
        "facets": {
            "sightingWeekFacet": {
                "type": "date",
                "path": "date",
                "boundaries": [ISODate("2022-01-01"),
                    ISODate("2022-01-08"),
                    ISODate("2022-01-15"),
                    ISODate("2022-01-22")],
                "default": "other"
            }
        }
    }
}
```



