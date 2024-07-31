The simplest data pipeline.

# Useful Docker commands

## build image using Dockerfile in current directory

```
docker build -t mypipeline:pandas .
```

## run docker image

```
docker run -it mypipeline:pandas
```

this pipeline.py expects an argument from command line which can be passed after the image name

```
docker run -it mypipeline:pandas monday
```

## Open shell in the container

```
docker exec -it <container_name_or_id> bash

```

## Running postgres in a container (in mac)

```
docker run -it \
 -e POSTGRES_USER="postgres" \
 -e POSTGRES_PASSWORD="postgres" \
 -e POSTGRES_DB="ny_taxi" \
 -v /Users/kishorneupane/Desktop/temp-practice/ny_taxi_postgres_data:/var/lib/postgresql/data \
 -p 5499:5432 \
 postgres:13
```

NOTE: I used this path (/Users/kishorneupane/Desktop/ny_taxi_postgres_data) because mac allows only few directories to be bind mounted by default (/Users, /Volumes, /tmp and /private). Otherwise, to use other directories, we would have to update file sharing preferences which can be done in docker desktop.

Now, we can use psql to query the database

```
psql -h 127.0.0.1 -p 5499 -U postgres -d ny_taxi
```

NOTE: I used port 5499 for my host because i already have an app called postgresapp which runs postgres server in 5432. So, basically to prevent the conflict. I was getting this error before i figured out it was due to the port conflict:
psql: error: connection to server at "127.0.0.1", port 5432 failed: FATAL: database "ny_taxi" does not exist
