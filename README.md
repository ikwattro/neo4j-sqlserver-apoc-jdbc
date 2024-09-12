# Neo4j load data from SQLServer with APOC

## Run

The Docker compose file includes SQL Server and Neo4j.

Run the compose file : 

```bash
docker compose up -d
```

Run the following command to initialise the tables in SQL Server ( it creates the movies graph but as tables :) )

```bash
docker exec -it sqlserver /opt/mssql-tools18/bin/sqlcmd -S localhost -U sa -P "npaEzszSALRH5q56372zGJ" -C -i /sql/init.sql
```

Go to the Neo4j browser on http://localhost:7474 and login with `neo4j/password`.

Run the following APOC procedures to read data from SQL Server 

```cypher
CALL apoc.load.jdbc('jdbc:sqlserver://sqlserver:1433;databaseName=movies;user=sa;password=npaEzszSALRH5q56372zGJ;encrypt=false', 'Person')
//
CALL apoc.load.jdbc('jdbc:sqlserver://sqlserver:1433;databaseName=movies;user=sa;password=npaEzszSALRH5q56372zGJ;encrypt=false', 'Movie')
//
CALL apoc.load.jdbc('jdbc:sqlserver://sqlserver:1433;databaseName=movies;user=sa;password=npaEzszSALRH5q56372zGJ;encrypt=false', 'ActedIn')
```