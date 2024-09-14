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
  hire_date DATE,
);
```

If you need to select a table:
```MySQL
select * from employees;
```
To rename a table:
```MySQL
rename table employees to workers;
```
To alter your table:
```MySQL
alter table employees 
add phone_number varchar(15);
```
To change a column name:
```MySQL
alter table employees
rename column phone_number to email;
```
To alter column type:
```MySQL
alter table employees
modify column email varchar(100);
```
To move a column:
```MySQL
alter table employees
modify email varchar(100)
after last_name;
```
OR
```MySQL
alter table employees
modify email varchar(100)
first;
```

To insert rows:
```MySQL
insert into employees
values (1, "Eugene", "Krabs", 25.50, "2023-01-02");

select * from employees;
```

To select specific columns:
```MySQL
select last_name, first_name from employees;
```
To select specific data:
```MySQL
select last_name, first_name from employees
where employee_id = 4;
```
Or:
```MySQL
select last_name, first_name from employees
where hourly_pay >= 15;
```

To update data:
```MySQL
update employees
set hourly_pay = 10.25
where employee_id = 6;
select * from employees;
```
To delete data (be sure to add a where clause, otherwise it will delete all of your data):
```MySQL
delete from employees
where employee_id = 6;
select * from employees;
```
To manually save each entry:
```MySQL
set autocommit = off;
```
To undo / rollback to the last step:
```MySQL
rollback;
```
To add in the current data / time:
```MySQL
insert into employees
values(current_date(), current_time(), NOW());
```
To make a column with a required value, simply add "not null". For example:
```MySQL
create table products(
  product_id INT,
  product_name varchar(25),
  price decimal (4, 2) **not null**
);
```
To add it to a full table that already exists:
```MySQL
alter table products
modify price decimal(4, 2) not null;
```

Checkpoint 50:04






