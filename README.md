# INSERT_ASSIGNMENT_SQL
create database insert_assignment;
use insert_assignment;
-- 1. Write a SQL statement to insert a record with your own value into the table countries against 
-- each column. 
-- Here in the following is the structure of the table countries. 
-- +--------------+---------------+------+-----+---------+-------+ 
-- | Field        
-- | Type          
-- | Null | Key | Default | Extra | 
-- +--------------+---------------+------+-----+---------+-------+ 
-- | COUNTRY_ID   | varchar(2)    | YES  |     | NULL    |       | 
-- | COUNTRY_NAME | varchar(40)   | YES  |     | NULL    |       | 
-- | REGION_ID    | decimal(10,0) | YES  |     | NULL    |       | 
-- +--------------+---------------+------+-----+---------+-------+  

create table countries(
country_id varchar(2),
country_name varchar(40),
region_id decimal(10,0)
);
insert into countries values("IN","Indore",12);
select * from countries;
desc countries;



-- 2. Write a SQL statement to insert one row into the table countries against the column country_id 
-- and country_name. 
-- Here in the following is the structure of the table countries. 
-- +--------------+---------------+------+-----+---------+-------+ 
-- | Field        
-- | Type          
-- | Null | Key | Default | Extra | 
-- +--------------+---------------+------+-----+---------+-------+ 
-- | COUNTRY_ID   | varchar(2)    | YES  |     | NULL    |       | 
-- | COUNTRY_NAME | varchar(40)   | YES  |     | NULL    |       | 
-- | REGION_ID    | decimal(10,0) | YES  |     | NULL    |       | 
-- +--------------+---------------+------+-----+---------+-------+  

insert into countries values("BP","Bhopal",10);
select * from countries;
-- 3. Write a SQL statement to create duplicate of countries table named country_new with all 
-- structure and data. 
-- Here in the following is the structure of the table countries. 
-- +--------------+---------------+------+-----+---------+-------+ 
-- | Field        
-- | Type          
-- | Null | Key | Default | Extra | 
-- +--------------+---------------+------+-----+---------+-------+ 
-- | COUNTRY_ID   | varchar(2)    | YES  |     | NULL    |       | 
-- | COUNTRY_NAME | varchar(40)   | YES  |     | NULL    |       | 
-- | REGION_ID    | decimal(10,0) | YES  |     | NULL    |       | 
-- +--------------+---------------+------+-----+---------+-------+  
create table country_new select * from countries;
-- insert into countries values("IN","Indore",12);
select * from country_new;


-- 4. Write a SQL statement to insert NULL values against the region_id column for a row of 
-- countries table. 
insert into countries values("JB","Jabalpur",null);
select * from countries;


-- 5. Write a SQL statement to insert 3 rows by a single insert statement. 
insert into countries values('MN','Mondsore',9),('KN','Khandwa',8),('RW','Reewa',7);
select * from countries;


-- 6. Write a SQL statement insert rows from country_new table to countries table. 
-- Here are the rows for the country_new table. Assume that the country's table is empty. 
-- +------------+--------------+-----------+ 
-- | COUNTRY_ID | COUNTRY_NAME | REGION_ID | 
-- +------------+--------------+-----------+ 
-- | C0001      | India        
-- |      
-- | C0002      | USA          
-- | C0003      | UK           
-- |      
-- 1001 | 
-- |      
-- 1007 | 
-- 1003 | 
-- +------------+--------------+-----------+ 
drop table countries;
drop table country_new;
create table country_new(
country_id varchar(20),
country_name varchar(40),
region_id decimal(10,0)
);
create table countries(
country_id varchar(20),
country_name varchar(40),
region_id decimal(10,0)
);
insert into country_new values(' C0001 ','India',1001),('C0002 ','USA ',1007),('C0003','UK',1003);
select * from country_new;
insert into countries select * from country_new;
select * from countries;

-- 7. Write a SQL statement to insert one row in jobs table to ensure that no duplicate value will be 
-- entered in the job_id column. 
create table jobs(
job_id varchar(10) unique,
job_title varchar(50),
min_salary decimal(10,0),
max_salary decimal(10,0)
);
insert into jobs values('MGR','FINANCE',10000,20000);
select * from jobs;


-- 8. Write a SQL statement to insert one row in jobs table to ensure that no duplicate value will be 
-- entered in the job_id column. 
insert into jobs values('DPMGR','FINANCE',5000,7000);
select * from jobs;
desc countries;


-- 9. Write a SQL statement to insert a record into the table countries to ensure that, a country_id 
-- and region_id combination will be entered once in the table. 
insert into countries (country_id,region_id) values("C0005",1111);
select * from countries;


-- 10. Write a SQL statement to insert rows into the table countries in which the value of 
-- country_id column will be unique and auto incremented.

alter table countries
modify column country_id varchar(50) unique ;
select * from countries;
insert into countries (country_id,country_name,region_id) values("C0006",'Japan',1112);


-- 11. Write a SQL statement to insert records into the table countries to ensure that the country_id 
-- column will not contain any duplicate data and this will be automatically incremented and the 
-- column country_name will be filled up by 'N/A' if no value assigned for that column. 
drop table countries;
create table countries(
country_id int(10) unique auto_increment,
country_name varchar(40) default 'N/A',
region_id decimal(10,0)
);
insert into countries(country_id,region_id) values(100,150);
insert into countries(country_name,region_id) values("india",120);
select * from countries;


-- 12. Write a SQL statement to insert rows in the job_history table in which one column job_id is 
-- containing those values which are exists in job_id column of jobs table. 
INSERT INTO job_history (employee_id, start_date, end_date, job_id, department_id)
SELECT s.employee_id, s.start_date, s.end_date, s.job_id, s.department_id
FROM staging_job_history s
WHERE EXISTS (
    SELECT 1
    FROM jobs j
    WHERE j.job_id = s.job_id
);


-- 13. Write a SQL statement to insert rows into the table employees in which a set of columns 
-- department_id and manager_id contains a unique value and that combined values must have 
-- existed into the table departments. 

INSERT INTO employees (employee_id, first_name, last_name, email, hire_date, job_id, salary, manager_id, department_id)
SELECT e.employee_id, e.first_name, e.last_name, e.email, e.hire_date, e.job_id, e.salary, e.manager_id, e.department_id
FROM employee e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
      AND d.manager_id = e.manager_id
);


-- 14. Write a SQL statement to insert rows into the table employees in which a set of columns 
-- department_id and job_id contains the values which must have exists into the table departments 
-- and jobs. 
INSERT INTO employees (employee_id, first_name, last_name, email, hire_date, job_id, salary, manager_id, department_id)
SELECT s.employee_id, s.first_name, s.last_name, s.email, s.hire_date, s.job_id, s.salary, s.manager_id, s.department_id
FROM staging_employees s
WHERE EXISTS (
    SELECT 1 FROM departments d WHERE d.department_id = s.department_id
)
AND EXISTS (
    SELECT 1 FROM jobs j WHERE j.job_id = s.job_id
);
