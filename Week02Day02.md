# Week02 Day 02

## AWS

amzon web services. a cloud provider like azure or gcp offering a variety of iaas, paas, saas, faas services over the web.

### types of aas

iaas: infrastructure as a service. ec2(elastic computing), a vm. a vm can be started and the database can be installed on the vm.
paas: product as a service. RDS, firebase, etc. just an instance of a product such as a database. less flexible than a vm but simpler to manage 
saas: dropbox, office, pega, salesforce, etc
faas: functions as a service. lambda, etc.

### security groups

defines what entities have access to the aws service. we define inbound and outbound rules.

- inbound:
  - who has access to the db
- outbound:
  - the db has access to whom

## SQL

what came before relational databases? hierarchical database models, where everything follwed a tree like structure.

in relational databases, data "structures" can have access to other data structures. currently we have established a connection to a cloud instance of a postgres db.

### schema

a database can have multiple schemas. they define a collection of db objects that are to be associated with a database, tables for instance.

### SQL
 structured query language. its syntax resembles a spoken language and is meant to be readable.
 
- sql is split up into subdomains or sublanguages:
  - DML: data manipulation lang:
    - insert
    - select
    - update
    - delete
    - the basic CRUD operations
  - DDL: data definition lang:
    - create
    - alter
    - drop
    - truncate
    - grant/revoke
  - TCL: transaction control lang
  - DCL: data control lang
  - DQL: data query lang

different database vendors have different implmentations for these languages, but they all generally follow this standard.

### DCL

used to provide privileges to users. for creating new logins and setting privileges/access control to the database

```sql
/* multiline
comment*/
-- DCL example
create role rando_login login password 'rando';
grant all privileges on schema public to rando_login;
```

### DDL

```sql
-- DDL example
-- creating a table with no columns is valid sql.
create table basic(
); 

create table if not exists upgraded(
  -- when creating a table, we only have to define column name and column datatype.
  -- sql convention is to use underscores rather than camelcase
  user_id int,
  user_name varchar(32),
);


create table if not exists planets(
-- columnname | columntype | constraints;
  planet_id serial primary key,
  planet_name varchar(32) not null unique,
  planet_description varchar(64) not null,
  has_rings boolean not null,
  number_of_moons smallint check(number_of_moons > -1)
);

-- deletes the table structure along with all data in it
drop table upgraded;
-- deletes data, but not the table structure
truncate table planets;

alter table if exists planets rename has_rings to rings;
```

### tangent about the postgres docs

ALTER TABLE [ IF EXISTS ] [ ONLY ] name [ * ] action [ list.... ]

bracketed clauses are optional, non braketed clauses are required for the query.

### dataypes

- int
- double
- varchar
- float
- float8
- timestamp
- char
- boolean
- full list at https://www.postgresql.org/docs/9.5/datatype.html

### DML and dql

```sql
insert into upgraded values(-10, 'bob');
insert into upgraded values(-10, null);

-- a serial insert query
insert into planets values(1, 'Mercury', 'Never too close', true,0);

-- spcified columns for data
insert into
  planets (planet_name, planet_description, rings, number_of_moons)
  values ('Venus', 'Getting a tad warm', false, 0);
  
-- alternatively
insert into planets (planet_name, planet_description, rings, number_of_moons) values
  ('Mercury', 'Never too close', true, 0),
  (...), --rest of the planets
  ;
```

### reading values from the table

```sql
select * from planets;

select planet_name, planet_description from planets;
```

### the `where` clause (DQL and DML)

you don't always want all of the data from the entire table, right?

some people might argue that a query is not DML, but is in fact DQL. this is dependent on vendor implementation and a matter of debate.

```sql
-- the where clause acts as a filter
select planet_name from planets where planet_name = 'Mercury';
select * from planets where planet_name = 'Mercury';

select planet_name from planets where rings=true;

-- and and or clause
select planet_name from planets where rings = true and number_of_moons > 20;
select planet_name from planets where tings = true or number_of_moons < 20;

-- the order by keywords, optionally ascending or descending
select * from planets order by planet_name desc;
```

### aliases

-- these do not affect the table structure, they only modify the view

```sql
select planet_name from planets as p where p.planet_id = 8;
-- now the entire record where the planet id is 8 will be referred to as 'p'

select planet_name as name from planets;
```

### updating

```sql
update planets set planet_description = 'very big' where planet_name='Jupiter';
-- this will update all info on the table
update planets set number_of_moons = 100;
-- very dangerous. make sure there is always a where clause.
-- dbeaver will warn you when you try to do this.
```

### deleting records

```sql
delete from planets where planet_id=9;

delete from planets;
-- again, don't forget a where clause
```

`delete from planets;` behaves like truncate, but the data storage is also deleted.
truncate leaves the data storage allocation of the table intact.
this makes truncate the much more resource efficient operation if you ever want to do this.
the deleted data is recoverable, but only if it was done in a transaction.

## assignment

pushed to github at https://github.com/2012reston/

work up to 2.7, go farther if you want.
chinook_database_setup_script.sql will set up the example database you'll work from. run it in dbeaver.
