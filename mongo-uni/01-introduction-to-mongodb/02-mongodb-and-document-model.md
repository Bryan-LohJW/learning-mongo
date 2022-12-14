# MongoDB Overview

## Content

 - How MongoDb is classfied and commonly used

 - How data is organized

 - How MongoDB relates to Atlas

## MongoDB

MongoDB is a general purpose document database, meaning it structures data in documents which are similar to JSON objects

Documents offer flexible and developer friendly way to work with data by matching storage with how we think in code

Has drivers for most major languages

## Document Model

Makes it easier to plan how application data will correspond to data in database

It can model data of any shape and structure, such as:

 - Key-value

 - Text

 - Geospatial

 - Time-series

 - Graph data

Only one format for using and storing data is more productive

### More on Document Model

Documents are displayed in JSON, and stored in database as `BSON` (Binary-JSON). BSON adds support for data types unavailable in JSON.

ObjectID is a special datatype in MongoDB that helps to uniquely identify documents and acts as the primary key. MongoDB will genetate the ObjectID if an inserted document doesn't include the _id field.

### Flexible schema model & Polymorphic data

These features allow us to store documents with different structures in the same collection

 - Documents may contain different fields

 - Fields may contain different types

A flexible schema allows for quick iteration and evolution, unlike a relational database where an addition of a single field will require major change

In MongoDB, only need to update classes to include new fields, and start inserting documents with the new schema

Optional schema validation sets constraints on the structure of documents as necessary



## Key terms

 - Document: The basic unit of data storage in MongoDB

 - Collection: A grouping of documents

 - Database: A container for collections

# MongoDB and Atlas

MongoDB is the core of Atlas, Atlas serves as a service layer for text search, data visualization and other features.

## Atlas Data Explorer

It is a tool for interacting and managing data from the Atlas UI

 - View, click on database and view collection. Able to look at databases, collections, and documents

 - Create, click on create database button to create new database. Within an existing database, can also create new collection. Inserting documents into collection, can select number of fields and change their datatypes and values

Can also edit and delete data, write and test queries on the Atlas UI