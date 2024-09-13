# MySQL-Tutorial

SQL = Structured Query Language

SQL is used to Create, Retrieve, Update, & Delete

Two types of databases: 

1) Relational (SQL) - Uses the concept of keys. It has rows & columns i.e. excel spreadsheet. 

2) Non-relational (NoSQL) - data is organized in any way other than a table i.e. json files, key value pairs, graph data structures, etc.

This tutorial focuses solely on relational databases.

Database Management Systems (DBMS) - workspaces that allow us to write SQL statements and work with our database(s). 

Common DBMS include:
<li>MySQL</li>
<li>Microsoft SQL Server</li>
<li>Oracle</li>
<li>PostgresSQL</li>
<li>Supabase (Uses PostgresSQL under the hood + additional features like authentication, storage, etc.)</li>

In this series we are of course going to focus on [MySQL](https://www.mysql.com/)

Follow the instructions in the previous link to install MySQL. 

Once installed, you can create a database with:

```MySQL
create database myDB;
```
Hit the lightning button to execute.

To use that database, either right click "Set as Default Schema" and select or use the following command:

```MySQL
use myDB;
```

To drop a database:
```MySQL
drop database myDB;
```

To set a database to read only:
```MySQL
alter datbase myDB read only = 1;
```
To change it out of read only:
```MySQL
alter datbase myDB read only = 0;
```

To create a table:
```MySQL
create table employees(
  employee_id INT,
  first_name VARCHAR(insert number of characters),
  last_name VARCHAR(50),
  hourly_pay DECIAML(5, 2),
  fire_date,
);
```

If you need to select a table:
```MySQL
select * from eployees;
```
To rename a table:
```MySQL
rename table employees to workers;
```
