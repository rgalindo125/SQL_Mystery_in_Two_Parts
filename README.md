# Employee Database: A Mystery in Two Parts

# Overview

Conduct a research project on employees of the corporation from the 1980s and 1990s. All that remain of the database of employees from that period are six CSV files.

Design the tables to hold data in the CSVs, import the CSVs into a SQL database, and answer questions about the data. In other words, perform the following:
   1. Data Madeling
   2. Data Engineering
   3  Data Analysis
   
# Objectives

# Data Modeling
Inspect the CSVs and sketch out an ERD of the tables using QuickDBD

![](https://github.com/rgalindo125/SQL_Mystery_in_Two_Parts/blob/master/QuickDBD-employee_db.png)

# Data Engineering
* Use the information to create a table schema for each of the six CSV files. Remember to specify data types, primary keys, foreign keys, and other constraints.
* Import each CSV file into the corresponding SQL table.

CREATE TABLE employees
(
    emp_no INT NOT NULL,
    birth_date DATE NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    gender VARCHAR(100) NOT NULL,
    hire_date DATE NOT NULL,
    PRIMARY KEY (emp_no)
);

CREATE TABLE departments
(
    dept_no VARCHAR(100) NOT NULL,
    dept_name VARCHAR(100) NOT NULL,
    PRIMARY KEY (dept_no),
    UNIQUE   	(dept_name)
);

CREATE TABLE dept_manager
(
    dept_no VARCHAR(100) NOT NULL,
    emp_no INT NOT NULL,
    from_date DATE NOT NULL,
    to_date DATE NOT NULL,
    FOREIGN KEY (emp_no)  REFERENCES employees (emp_no),
    FOREIGN KEY (dept_no) REFERENCES departments (dept_no),
    PRIMARY KEY (emp_no,dept_no)
);

CREATE TABLE dept_emp
(
    emp_no INT NOT NULL,
    dept_no VARCHAR(100) NOT NULL,
    from_date DATE NOT NULL,
    to_date DATE NOT NULL,
    FOREIGN KEY (emp_no)  REFERENCES employees   (emp_no),
    FOREIGN KEY (dept_no) REFERENCES departments (dept_no),
    PRIMARY KEY (emp_no,dept_no)
);

CREATE TABLE titles
(
    emp_no INT NOT NULL,
    title VARCHAR(100) NOT NULL,
    from_date DATE NOT NULL,
    to_date DATE,
    FOREIGN KEY (emp_no) REFERENCES employees (emp_no),
    PRIMARY KEY (emp_no,title, from_date)
);

CREATE TABLE salaries
(
    emp_no INT NOT NULL,
    salary INT NOT NULL,
    from_date DATE NOT NULL,
    to_date DATE NOT NULL,
    FOREIGN KEY (emp_no) REFERENCES employees (emp_no),
    PRIMARY KEY (emp_no, from_date)
);
