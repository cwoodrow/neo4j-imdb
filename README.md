# IMDB Dataset for Neo4J

This is a Dataset from [IMDB](https://www.imdb.com/) prepared to be ingested in [Neo4J](https://neo4j.com/).

## Usage 

Step 1: Consolidate the files:

```bash
# we need to cat role files (split due to github limits)
cat ./imdb-data/roles.split.* > ./imdb-data/roles.csv
```

Step 2: Import the files into a new database called `imdb`. If the database file already exist, you must add the `--force` flag so that it will be re-created upon import.


> NOTE: this command is for Neo4J version 4+.

```bash
$NEO4J_HOME/bin/neo4j-admin import              \    # --force (if the db file exists) 
    --database=imdb                             \
    --nodes=Movie=./imdb-data/movies.csv        \
    --nodes=Actor=./imdb-data/actors.csv        \
    --relationships=./imdb-data/roles.csv

$NEO4J_HOME/bin/neo4j start
```

Then go to [http://localhost:7474/browser/](http://localhost:7474/browser/) or open your Neo4J Desktop Application.

> Note that the previous version 3 of neo4j uses a slighly different syntax for providing node and relationship information. 
> 
> ```bash
> $NEO4J_HOME/bin/neo4j-admin import           \
>   --database imdb                            \
>   --nodes:Movie   ./imdb-data/movies.csv     \
>   --nodes:Actor   ./imdb-data/actors.csv     \
>   --relationships ./imdb-data/roles.csv

### First query

Here you can make your first query: 

```cypher
MATCH (kevin:Actor{name:"Bacon, Kevin (I)"})
return kevin;
```

## Installation

You can install neo4j either as a standalone desktop application (which starts neo4j server), or as a set of CLI tools. 

Download NEO4J from [here](https://neo4j.com/download-center/#releases) (choose `Community Server`) and unzip it to your favorite target (we'll call it `$NEO4J_HOME` from now on). You'll also need Java 8+ on your computer.

### Alternatives

Open this URL — https://neo4j.com/download-center/#community and download the appropriate software. Run the installer, or copy/drag the folder to where keep your applications.

#### Desktop Application

If you decide to use the Neo4J Desktop Application, keep in mind that it starts the neo4j server when opened:

```bash
brew install cask homebrew/cask/neo4j
open /Applications/Neo4j\ Desktop.app
``` 

To get only the CLI tools installed:

```bash
brew install neo4j
```

This should install the tools in `/usr/local` (this would also be the value of `$NEO4J_HOME` env variable). In this way you can find all executable commands in `$NEO4J_HOME/bin` (which you may want to add to your `$PATH`), and the database files in `NEO4J_HOME/data/databases`.

### Types of Installer

When you download the desktop application, it will start the  server when started, and will prompt you whether to keep the server running upon closing.

If you only installed the CLI you may need to create the database and run the neo4j process separately.


## Disclaimer

Data from IMDB can be a bit `tricky`. For example, "Kevin Bacon" is "Bacon, Kevin (I)". Don't ask me why, anyway it is consitent with actual [IMDB search reesults](https://www.imdb.com/find?ref_=nv_sr_fn&q=kevin+bacon&s=all).

## Original Data 

Original Data may be found [here](https://datasets.imdbws.com/).

## License 

© 2018+ Chris Woodrow
MIT License

