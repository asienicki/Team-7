go to folder with path \containers_artifacts\src\poi\

run command to build image:
```
docker build --no-cache --build-arg IMAGE_VERSION="1.0" --build-arg IMAGE_CREATE_DATE="`date -u +"%Y-%m-%dT%H:%M:%SZ"`" --build-arg IMAGE_SOURCE_REVISION="`git rev-parse HEAD`" -f Dockerfile -t "tripinsights/poi:1.0" .
```

create custom network bridge in docker:
```
docker network create -d bridge poinetwork
```

we need database for our application so we need to create one:
```
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Passw0rd12345!" -e "MSSQL_DATABASE=mydrivingDB"  --network poi -p 1733:1433 --name SqlServer --hostname SqlServer -d mcr.microsoft.com/mssql/server:2017-latest
```

If succeeded it's time to create database and fill it with data.
Use SQLCMD, SQL ManagmentStudio or Azure Studio and create database manually with name: mydrivingDB

to fill data run container:
```
docker run --network poi -e SQLFQDN=SqlServer -e SQLUSER=sa -e SQLPASS=Passw0rd12345! -e SQLDB=mydrivingDB registrywqs1862.azurecr.io/dataload:1.0
```

now we can create container for POI application:
```
docker run -d -p 8080:80 --network poi --name poinetwork -e SQL_PASSWORD=Passw0rd12345! -e SQL_SERVER=SqlServer -e SQL_USER=sa -e SQL_DBNAME=mydrivingDB -e ASPNETCORE_ENVIRONMENT=Local tripinsights/poi:1.0
```

check if POI is working and run:
```
curl -i -X GET 'http://localhost:8080/api/poi/trip/ea2f7ae0-3cef-49cb-b7d1-ce972113120c'
```

Should return json with data.

We have here 3 steps - create sql container, manual create database and filldatabase with data - we could wrap it up as single docker-compose - but for now - we can't do that because SQL_DatabaseName is not current supported.

Only for fun - I created 2 separated docker-compose.yml in catalog: composes. For me it's more readable than command.