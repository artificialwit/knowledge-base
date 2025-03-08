## Postgre SQL basic

## installlation from website and default
  - https://www.enterprisedb.com/postgresql-tutorial-resources-training-1?uuid=69f95902-b451-4735-b7e4-1b62209d4dfd&campaignId=postgres_rc_17
  - after insatllation search in windows as PgAdmin to run the Postgre Console, it is just like SQL Server managament Studio
  - We have command from also for PostgreSQL, that is SQL Shell (pgsql)
  - defaults
    - default connection/server is localhost,
    - default database created is postgres
    - default user of that database is postgres
    - default password would be same as we entered on installation time
### Common Command
  - SELECT datname FROM pg_database
  - SERIAL data type for Auto increment
  - currval('index_name_of_table')
  - nextval('index_name_of_table') , it store in table as default formula to get the next auto number in case of insert
### References
- https://www.youtube.com/watch?v=cnzka7kF5Zk
