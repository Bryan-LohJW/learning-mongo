# MongoDB Connection

## Connection String

Allows connection to cluster to work with data, it describes the host to connect to, and connection options.

Connection string allows for connection from shell, MongoDB compass, or any other applications

Two formats for connection

 - Standard format, used for standalone clusters, replica sets, or sharded clusters

 - DNS seed list format, provides a DNS server list to connection string, gives more flexibility of deployment. and give ablility to change servers in rotation without reconfiguring clients

To locate string

 - Look at database deployment > connect

 - Select the connection as required

 - Follow the steps to retrieve the string

Sample string: 

> mongodb+srv://<username>:<password>@cluster0.usqsf.mongodb.net/?retryWrites=true&w=majority

 - `mongodb` identifies it as a mongodb connection string

 - `+srv` tells mongodb to use seed list and security

 - `username & password`

 - `@cluster0...` is the host and port number, port number defaults to 27017

 - the rest is the additional options

## Connect to the MongoDB Shell

Connect using the command given in the website, and use mongosh command after installing it

The shell is based off JavaScript, thus can use things like variables, functions, conditionals, loops, and control flow statements

## MongoDB Compass

Compass is a GUI that allows us to query and analyze our data, and compose aggregation pipelines

Download MongoDB Compass, use the connect to Compass selection to retrieve the URI and replace the password. From Compass, we can view queries, databases, and performace. On the left column, able to view collections and documents

## MongoDB Drivers

Drivers allows connection to database using the programming language of our choice, it uses a connection string to connect to database.

mongodb.com/docs/drivers // convert to link

The documentation will guide through the process of setting up the connection and usage examples.

mongodb.com/developer // for learning by doing

Or can use MongoDB University to learn the specific driver for language of our choice

## Troubleshooting

### Connection issues

Most connection issues stem from MongoDB protecting our data. For example incorrect user authentication will not be allowed access.

 - One possible fix is to whitelist IP address

 - Recheck connection string is accurate, including password