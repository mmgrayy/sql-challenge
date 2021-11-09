-- drop table employees;
-- drop table departments;
-- drop table dept_emp;
-- drop table dept_manager;
-- drop table salaries;
-- drop table titles;

-- Create your tables:
--#1 Employees
-- **make all types not null to be safe
create table employees(
    emp_no int not null,
	emp_title_id varchar not null,
    birth_date date not null,
    first_name varchar not null,
    last_name varchar not null,
    gender varchar not null,
    hire_date date NOT NULL,
-- Primary Key: Employee Number
	PRIMARY KEY (emp_no)
);
--Import employee csv
SELECT * from employees;

--#2 Department
create table departments (
    dept_no varchar not null,
    dept_name varchar not null,
--Primary key: Department Number
	PRIMARY KEY (dept_no)
);
--Import Department csv
select * from departments;

--#3 Department Employees
create table dep_employees (
    emp_no int not null,
	dept_no varchar not null,
--Foreign Keys: Employee Number & Department Number respectively 
	FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
	FOREIGN KEY (dept_no) REFERENCES departments(dept_no)
);
select * from dep_employees;

--#4 Department Manager
create table dep_manager (
    dept_no varchar not null,
    emp_no int not null,
--Foreign Key: same as above
	foreign key (dept_no) references departments(dept_no),
	foreign key (emp_no) references employees(emp_no)
	
);
--Import csv

SELECT * from dep_manager;

--#5 Salaries
create table salaries (
    emp_no int not null,
	salary int not null,
--Foreign KEY: employee number 
	FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);
--IMPORT csv 
SELECT * from Salaries;

--#6
create table titles (
	title_id varchar not null,
    title varchar not null

);
--IMPORT csv
SELECT * from titles;







--ANALYSIS

-- 1. employee number, last name, first name, gender, and salary.
select employees.emp_no, employees.last_name, employees.first_name, employees.gender,
salaries.salary
FROM employees
INNER JOIN salaries ON
employees.emp_no = salaries.emp_no;



-- 2. employees who were hired in 1986.
SELECT emp_no, first_name, last_name, hire_date from employees
WHERE hire_date >= '1985-12-31'
AND hire_date < '1987-01-01';



-- 3.manager of each department w/: 
		-- department number, department name, the manager's employee number, 
		-- last name, first name.
SELECT dep_manager.dept_no, 
	   departments.dept_name,
	   dep_manager.emp_no,
	   employees.last_name,
	   employees.first_name
FROM dep_manager
INNER JOIN departments ON
dep_manager.dept_no = departments.dept_no
INNER JOIN employees ON
dep_manager.emp_no = employees.emp_no;




-- 4. List the department of each employee with the following information: 
	-- employee number, last name, first name, and department name.
SELECT employees.emp_no, 
	   employees.last_name, 
	   employees.first_name,
	   departments.dept_name
FROM employees
INNER JOIN dep_manager ON
employees.emp_no = dep_manager.emp_no
INNER JOIN departments ON
dep_manager.dept_no = departments.dept_no;




-- 5. List all employees whose first name is "Hercules" and last names begin with "B."
SELECT * FROM employees
WHERE first_name = 'Hercules'
AND last_name LIKE 'B%';




-- 6. List all employees in the Sales department, 
	--including their employee number, last name, first name, and department name.
SELECT 	employees.emp_no, 
		employees.last_name, 
		employees.first_name, 
		departments.dept_name
FROM employees 
JOIN dep_employees
ON employees.emp_no = dep_employees.emp_no
INNER JOIN departments 
AS departments 
ON dep_employees.dept_no = departments.dept_no
WHERE dept_name = 'Sales';



-- 7. List all employees in the Sales and Development departments, 
	-- including their employee number, last name, first name, and department name.
SELECT 	employees.emp_no, 
		employees.last_name, 
		employees.first_name, 
		departments.dept_name
FROM employees 
JOIN dep_employees
ON employees.emp_no = dep_employees.emp_no
INNER JOIN departments 
AS departments 
ON dep_employees.dept_no = departments.dept_no
WHERE dept_name = 'Sales' 
OR dept_name = 'Development'




-- 8. In descending order, list the frequency count of employee last names, 
	-- i.e., how many employees share each last name.
SELECT last_name, COUNT(last_name) FROM employees
GROUP BY last_name
ORDER BY count(last_name) desc;
