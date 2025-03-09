## Postgre SQL basic
### Environment variable settings
  - System Variables
    - Variable Name: PGHOME
    - Vairable Valule:  C:\Program Files\PostgreSQL\17\bin
  - Command
    - use pgxnclient inplace of pgxn 
### Entesions
  - *Make* is also must be installed to run the make file 
  - Make sure your have installed C++ tools, from microsoft visual studio installer, these must be below
  - Now follow the window steps
    - https://github.com/pgvector/pgvector
  - PG_NET
    - Use Installation instruction of pgvector
    - call "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvars64.bat"
    - git clone https://github.com/supabase/pg_net.git
    - cd pg_net
    - set "PGROOT=C:\Program Files\PostgreSQL\17"
    - make && make install
  - create extension if not exists pg_net
  - create extension if not exists vector
  - 
## installlation from website and default
  - https://www.enterprisedb.com/postgresql-tutorial-resources-training-1?uuid=69f95902-b451-4735-b7e4-1b62209d4dfd&campaignId=postgres_rc_17
  - after insatllation search in windows as PgAdmin to run the Postgre Console, it is just like SQL Server managament Studio
  - We have command from also for PostgreSQL, that is SQL Shell (pgsql)
  - defaults
    - default connection/server is localhost,
    - default database created is postgres
    - default user of that database is postgres
    - default password would be same as we entered on installation time
    - Default schema is public just like dbo in MS SQL. all table, procedure etc. must be a part of a schema, just like MS SQL
      
### Language
  - **just PL/SQL, in postgre it calls PL/pgSQL**. It allows users to write functions, triggers, and procedural code within the database using control structures like loops, conditions, and error handling
  - **PL/Python – Allows writing functions in Python.**
## Extension installation
  - visit https://pgxn.org/
  - search your extension and install
### Common Command
  - SELECT datname FROM pg_database
  - SERIAL data type for Auto increment
  - currval('index_name_of_table')
  - nextval('index_name_of_table') , it store in table as default formula to get the next auto number in case of insert
  - LIMIT 5 , to get top 5 rows from select command, it must be last command
  - Use CONCAT(firstName, LastName) , to concatinate two string, it is better way
  - Use CONCAT_WS(' ', firstName, LastName) , to concatinate two string with seperator, it is better way
### References
- https://www.youtube.com/watch?v=cnzka7kF5Zk
