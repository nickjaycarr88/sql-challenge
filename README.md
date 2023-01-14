# sql-challenge
### It’s been two weeks since you were hired as a new data engineer at Pewlett Hackard (a fictional company). Your first major task is to do a research project about people whom the company employed during the 1980s and 1990s. All that remains of the employee database from that period are six CSV files.

### For this project, you’ll design the tables to hold the data from the CSV files, import the CSV files into a SQL database, and then answer questions about the data. That is, you’ll perform data modelling, data engineering, and data analysis, respectively.
### List the employee number, last name, first name, sex, and salary of each employee.
---
## Data Analysis
#### List the employee number, last name, first name, sex, and salary of each employee.
```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.sex,salaries.salary 
FROM employees
JOIN salaries
ON salaries.emp_no = employees.emp_no
```
#### List the first name, last name, and hire date for the employees who were hired in 1986.
```sql
SELECT employees.first_name, employees.last_name, employees.hire_date
FROM employees
WHERE hire_date BETWEEN '1986-01-01' AND '1986-12-31';
```
#### List the manager of each department along with their department number, department name, employee number, last name, and first name.
```sql
SELECT dept_manager.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name
FROM employees
JOIN dept_manager
ON employees.emp_no=dept_manager.emp_no
JOIN departments
ON dept_manager.dept_no=departments.dept_no;
```
#### List the department number for each employee along with that employee’s employee number, last name, first name, and department name.
```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM employees
JOIN dept_emp
ON employees.emp_no=dept_emp.emp_no
JOIN departments
ON dept_emp.dept_no=departments.dept_no
```

#### List the first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B.
```sql
SELECT employees.first_name, employees.last_name, employees.sex
FROM employees
WHERE first_name = 'Hercules' AND last_name LIKE 'B%';
```
#### List each employee in the Sales department, including their employee number, last name, and first name.
```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM employees
JOIN dept_emp
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no=departments.dept_no
WHERE departments.dept_name = 'Sales'
```
#### List each employee in the Sales and Development departments, including their employee number, last name, first name, and department name.
```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM employees
JOIN dept_emp
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no=departments.dept_no
WHERE departments.dept_name = 'Sales' OR departments.dept_name = 'Development'

```
#### List the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name).
```sql
SELECT last_name, COUNT(last_name) AS frequency 
FROM employees
GROUP BY last_name
ORDER BY frequency DESC;
```
---
## Table Schema
1[Image Link](https://github.com/nickjaycarr88/sql-challenge/blob/main/sql_challenge_schema.png)