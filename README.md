# sql-challenge
#Background
It is a beautiful spring day, and it is two weeks since you have been hired as a new data engineer at Pewlett Hackard. Your first major task is a research project on employees of the corporation from the 1980s and 1990s. All that remain of the database of employees from that period are six CSV files.

#Objectives
design the tables to hold data in the CSVs, import the CSVs into a SQL database, and answer questions about the data using:

#Data Engineering
* Use the information you have to create a table schema for each of the six CSV files. Remember to specify data types, primary keys, foreign keys, and other constraints.

  * For the primary keys check to see if the column is unique, otherwise create a [composite key](https://en.wikipedia.org/wiki/Compound_key). Which takes to primary keys in order to uniquely identify a row.
  * Be sure to create tables in the correct order to handle foreign keys.

* Import each CSV file into the corresponding SQL table. **Note** be sure to import the data in the same order that the tables were created and account for the headers when importing to avoid errors.

#Data Analysis
Once you have a complete database, use queries to answer the following questions:

1. List the following details of each employee: employee number, last name, first name, sex, and salary.

select employees.emp_no, employees.last_name, employees.first_name, employees.gender,
salaries.salary
FROM employees
INNER JOIN salaries ON
employees.emp_no = salaries.emp_no;

2. List first name, last name, and hire date for employees who were hired in 1986.

SELECT emp_no, first_name, last_name, hire_date from employees
WHERE hire_date >= '1985-12-31'
AND hire_date < '1987-01-01';

3. List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name.

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

4. List the department of each employee with the following information: employee number, last name, first name, and department name.

SELECT employees.emp_no, 
	   employees.last_name, 
	   employees.first_name,
	   departments.dept_name
FROM employees
INNER JOIN dep_manager ON
employees.emp_no = dep_manager.emp_no
INNER JOIN departments ON
dep_manager.dept_no = departments.dept_no;

5. List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."

SELECT * FROM employees
WHERE first_name = 'Hercules'
AND last_name LIKE 'B%';

6. List all employees in the Sales department, including their employee number, last name, first name, and department name.

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

7. List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.

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

8. In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.
SELECT last_name, COUNT(last_name) FROM employees
GROUP BY last_name
ORDER BY count(last_name) desc;


