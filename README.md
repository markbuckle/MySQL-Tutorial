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
To add in new values:
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

How to check a table/values against a limit:
```MySQL
alter table employees
add constraint chk_hourly_pay check (hourly_pay >= 10.00);
```

To drop a check:
```MySQL
alter table employees
drop check chk_hourly_pay;
```

To add a default value to a column:
```MySQL
create table products
  product_id int,
  product_name varchar(25),
  price decimal (4, 2) default 0
);
```
Or:
```MySQL
alter table products
alter price set default 0;
```

Primary Keys are unique identifiers. 

To set a primary key to a new table:
```MySQL
create table transactions(
  transaction_id int primary key,
  amount decimal(5, 2)
);
```
To add a primary key to an existing table:
```MySQL
alter table transactions
add constraint
primary key(transaction_id);
```
To add auto-increment, you can only do it to a primary key:
```MySQL
create table transactions(
  transaction_id int primary key auto_increment,
  amount decimal(5, 2)
);
```
And it will continue to auto-increment when you add in new values:
```MySQL
insert into transcations (amount)
values(4.99);
```
A foreign is is a primary key from one table that is being used in another table. 

To create a foreign key, use this as an example:
```MySQL
create table transactions(
  transaction_id int primary key auto_increment,
  amount decimal(5, 2)
  customer_id int,
  foregin key(customer_id) references customers(customer_id),
);
```

Before attempted to delete a foreign key, make sure to:
```MySQL
set foreign_key_checks = 0;

delete from customers
where customer_id = 4;
```

Once a a foreign key is deleted, we need to delete it from our current table (i.e. transacitons), you'll need to recreate the table like this:
```MySQL
create table transactions(
  transaction_id int primary key auto_increment,
  amount decimal(5, 2)
  customer_id int,
  foregin key(customer_id) references customers(customer_id),
  on delete set null
);
```
There's two differen't ways to delete a foreign key (aka on delete):
1) replace foreign key with null
```MySQL
on delete set null
```
2) delete entire row
Or: 
```MySQL
on delete cascade
```
Another way to do this might look like:
```MySQL
alter table transactions
add constraint fk_transactions_id
foreign key(customer_id) references customers(customer_id)
on delete cascade;
```

A stored procedure is prepared/verbose SQL code that you can save / bootstrap.

To turn code into a stored procedure:
```MySQL
delimiter $$
create procedure function_name()
begin
  <enter verbose code here>;
end $$
delimiter ;
```
To invoke the stored procedure. You can also pass data into the function parenthesis if you want to invoke a particular id within the function.
```MySQL
call function_name(1);
```
A trigger is when an event happens, do something. Ex. (insert, update or delete). It can check data, handle errors or audit tables.
Example:
Step 1:
```MySQL
alter table employees
add column salary decimal(10, 2) after hourly_pay;
```
Step 2:
```MySQL
update employees
set salary = hourly_pay * 2,080 (work hours in a typical year)
```
Step 3 (create the trigger):
```MySQL
create trigger before_hourly_pay_update
before update on employees
for each row
set NEW.salary = (NEW.hourly_pay * 2080);
```
Step 4:
```MySQL
show triggers;
```
Step 5 (update your trigger):
```MySQL
update employees
set hourly_pay = hourly_pay + 1;
```


