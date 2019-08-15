# Migrate Production Data to Staging

## How not to
The tempting solution here is to try to create the staging database using production as a template.
```
CREATE DATABASE targetdb 
WITH TEMPLATE sourcedb;
```

But if the database is production, you'll likely get the error:
```
ERROR:  source database "target_db" is being accessed by other users
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

## Bonus
Strip the extensions and ownership from the pg dump using the following format:
```
pg_dump -U [user] -h [production_server] \
--format=plain --no-owner --no-acl [source_db]  | \
sed -E 's/(DROP|CREATE|COMMENT ON) EXTENSION/-- \1 EXTENSION/g' > backup.sql
```

#### Resources
http://www.postgresqltutorial.com/postgresql-copy-database/
