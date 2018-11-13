# IMDB Dataset for Neo4J

This is a Dataset from [IMDB](https://www.imdb.com/) prepared to be ingested in [Neo4J](https://neo4j.com/).

## Usage 

Download NEO4J from [here](https://neo4j.com/download-center/#releases) (choose `Community Server`) and unzip it to your favorite target (we'll call it `$NEO4J_HOME` from now on). You'll also need Java 8+ on your computer.

```
# we need to cat role files (splitted due to github limits)
cat ./imdb-data/roles.split.* > ./imdb-data/roles.csv

$NEO4J_HOME/bin/neo4j-admin import --nodes:Movie ./imdb-data/movies.csv --nodes:Actor ./imdb-data/actors.csv --relationships ./imdb-data/roles.csv

$NEO4J_HOME/bin/neo4j start
```

Then go to [http://localhost:7474/browser/](http://localhost:7474/browser/).

## First query

Here you can make your first query : 

```
MATCH (kevin:Actor{name:"Bacon, Kevin (I)"})
return kevin;
```

## Disclamer 

Data from IMDB can be a bit `tricky`. For example, "Kevin Bacon" is "Bacon, Kevin (I)". Don't ask me why, anyway it is consitent with actual [IMDB search reesults](https://www.imdb.com/find?ref_=nv_sr_fn&q=kevin+bacon&s=all).

## Original Data 

Orifinal Data may be found [here](https://datasets.imdbws.com/).