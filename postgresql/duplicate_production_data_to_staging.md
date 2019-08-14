# Migrate Production Data to Staging

## How not to
The tempting solution here is to try to create the staging database using production as a template.
```
CREATE DATABASE targetdb 
WITH TEMPLATE sourcedb;
```

But if the database is production, you'll likely get the error:
```
ERROR:  source database "registry-app_production" is being accessed by other users
DETAIL:  There are 4 other sessions using the database.
```

## How I've solved this
What I'm going to do instead is run pg_dump and then populate a clean version of the staging db with this file.
```
pg_dump -h [production_server] -U [user] -O [source_db] -f backup.sql
psql -h [production_server] -U [user] -d [target_db] -f backup.sql
```

## Pitfalls
- You have to delete current staging db completely and start from scratch
- Large db backups take a while cross server like this. A solution within the server would be better.

#### Resources
http://www.postgresqltutorial.com/postgresql-copy-database/