Welcome to XBOX DataStax Hands On Lunch & Learn
===================
![icon](http://i.imgur.com/FoIOBlt.png)
![icon](http://imgur.com/Dq5iCgf)

In this session, you'll learn all about DataStax Enterprise. It's a mix between presentation and hands-on. This is **obviously** your reference for the hands-on content. Feel free to bookmark this page for future reference!


Hands On Setup
-------------

We have an 5 node cluster for you to play with! The cluster is currently running in both **search** and **analytics** mode so you can take advantage of both Spark and Solr on your Cassandra data.

// To SSH into the cluster:
```
ssh datastax@ipaddress
```
// You can login to any of these nodes

```
node 1 (dc0vm0): 138.91.146.245 / 10.0.0.7
Node 2 (dc0vm1): 138.91.145.32 / 10.0.0.6
Node 3 (dc0vm2): 138.91.148.247 / 10.0.0.8
Node 4 (dc0vm3): 138.91.149.147 / 10.0.0.9
Node 5 (dc0vm4): 138.91.149.184 / 10.0.0.5
password: C@ssandra
```

#### UI's you'll want to play around with

 - OpsCenter: http://138.91.148.235:8888
 - Spark Master: http://138.91.146.245:7080
   - then click "Back to Master"
 - Solr UI: http://138.91.146.245:8983/solr/

#### Connecting to the cluster from DevCenter
- Simply add a new connection
- Enter a name for your connection
- Enter any of the ip's from above as a contact host
- Profit.

![DevCenter How To](http://i.imgur.com/8zwzmDj.png)


----------


Hands On DSE Cassandra
-------------------

Cassandra is the brains of DSE. It's an awesome storage engine that handles replication, availability, structuring, and of course, storing the data at lightning speeds. It's important to get yourself acquainted with the Cassandra to fully utilize the power of the DSE Stack.

#### Creating a Keyspace, Table, and Queries

Try the following CQL commands in DevCenter. In addition to DevCenter, you can also use **CQLSH** as an interactive command line tool for CQL access to Cassandra. Start CQLSH like this:

```
cqlsh 127.0.0.1
```
> Make sure to replace 127.0.0.1 with the IP of the respective node

Let's make our first Cassandra Keyspace!

```
CREATE KEYSPACE <Enter your name> WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3 };
```

And just like that, any data within any table you create under your keyspace will automatically be replicated 3 times. Let's keep going and create ourselves a table. You can follow my example or be a rebel and roll your own.

```
CREATE TABLE <yourkeyspace>.sales (
        name text,
        time int,
        item text,
        price double,
        PRIMARY KEY (name, time)
) WITH CLUSTERING ORDER BY ( time DESC );
```

> Yup. This table is very simple but don't worry, we'll play with some more interesting tables in just a minute.
