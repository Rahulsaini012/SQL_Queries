create Database:[using_create_command]
create database xcompany;
using company;
Create table Departments:[using create command]
create table if not exists Departments( DepartmentId int primary key, DepartmentName varchar(50), Location varchar(30));

Insert values into Departments Table:[using insert command]
insert into Departments(DepartmentId,DepartmentName,Location) values (1, 'IT', 'New York'), (2, 'HR', 'London'), (3, 'Sales', 'San Francisco'), (4, 'Finance', 'Sydney');

Showcase Departments Table:[using select command]
select * from Departments;

Result:
Departments

Create table Employee:[using create command]
create table Employee( EmployeeId int primary key, FirstName varchar(30), LastName varchar(30), DepartmentId int, JobTitle varchar(30), Salary decimal(10,2), HireDate date, ManagerId int, foreign key (DepartmentId) references Departments(DepartmentId));

Insert values into Employee Table:[using insert command]
insert into Employee(EmployeeId,FirstName,LastName,DepartmentId,JobTitle,Salary,HireDate,ManagerId) values (1, 'John', 'Doe', 1, 'Software Engineer', 85000, '2020-05-10', NULL), (2, 'Jane', 'Smith', 2, 'HR Manager', 95000, '2018-07-20', NULL), (3, 'Alice', 'Brown', 1, 'DevOps Engineer', 78000, '2021-02-15', 1), (4, 'Bob', 'Johnson', 3, 'Sales Executive', 65000, '2019-11-05', NULL), (5, 'Charlie', 'Davis', 1, 'QA Engineer', 72000, '2022-03-12', 1), (6, 'Emily', 'White', 4, 'Financial Analyst', 88000, '2020-09-01', NULL), (7, 'Michael', 'Green', 1, 'Software Engineer', 85000, '2021-06-25', 1), (8, 'Sarah', 'Lee', 2, 'HR Specialist', 62000, '2021-08-30', 2);

create table Employee1:[Using_create_command]
create table employee1( EmployeeID varchar(13),name varchar(30), department varchar(30),salary int);

insert into employee1 values ("s101","Avantika","DA",50000), ("s102","Anu","DS",38000), ("s103","Sna","NS",25000), ("s104","briyan","DA",38000);

Create table orders:[using_create_command]
create table orders(customerID varchar(30),OrderID int,OrderDate int,Totalamount int); insert into orders values ("R101",101,1-01-2025,2000), ("R102",102,2-01-2025,4000), ("R103",103,3-01-2025,5000);

Showcase Employee Table:[using select command]
select * from Employee;

Result:
Employee

Query 1) Find the Second Highest Salary
Solution:

select max(salary)as second_highest_salary from employee where salary<(select max(salary) from employee);

Result

output

Query 2) Retrieve names of employees whose names start with "A" and end with "n":
Solution:

select FirstName,LastName,JobTitle,Salary from employee where FirstName like 's%h';

Result

output 1

Query 3) Display the total count of employees grouped by their department:
Solution:

select JobTitle, COUNT(*) AS EmployeeCount from Employee group by JobTitle;

Result

output 2

Query 4) Retrieve the list of duplicate records in a table:
Solution:

select JobTitle, COUNT() from Employee group by JobTitle having count() > 1;

Result

output3

Query 5) List all employees and their departments (including employees with no orders):
Solution:

select Employee.EmployeeID, Employee.FirstName, Departments.DepartmentID, Departments.DepartmentName from Employee left join Departments on Employee.EmployeeID = Departments.DepartmentID;

Result

output4

Query 6) Find the maximum, minimum, and average salary of employees in each department:
Solution:

select JobTitle, MAX(Salary) AS MaxSalary, MIN(Salary) AS MinSalary, AVG(Salary) AS AvgSalary from Employee group by JobTitle;

Result

output 5

Query 7) Fetch names of employees who earn more than the average salary in their jobtitle:
Solution:

select FirstName,LastName,Salary from Employee where Salary > (select avg(Salary) from Employee where JobTitle = Employee.JobTitle);

Result

output 6

Query 8) Fetch the 3 jobtitle:
Solution:

select EmployeeID, FirstName, Salary from Employee order by Salary desc limit 3;

Result

output7

Query 9) Calculate the running total of salaries:
Solution:

select EmployeeID, FirstName, LastName, Salary, SUM(Salary) over (order by Salary) as RunningTotal from Employee;

Result

output 8

Query 10) Fetch EmployeeId that is distinct:
Solution:

select EmployeeID, JobTitle from Employee where EmployeeID not in(select distinct DepartmentID from Departments);

Result

output 9

Query 11) To list Employee hired in the year 2021:
Solution:

select EmployeeId, FirstName, HireDate from Employee where year(HireDate) = 2021;

Result

output 10

Query 12) Find the EmployeeId with highest average salary:
Solution:

select EmployeeId, AVG(Salary) AS AvgSalary from Employee group by EmployeeId having avg(Salary) = (select max(AvgSalary) from (select EmployeeId, AVG(Salary) AS AvgSalary from Employee group by EmployeeId) as Sub);

Result

output 11

Query 13) Find employees whose salary is greater than the jobtitle average:
Solution:

select FirstName, Salary, JobTitle frm Employee where Salary > (select AVG(Salary) from Employee where JobTitle = Employee.JobTitle);

Result

output 12

Query 14) To find the departmentid according to jobtitle from departments table:
Solution:

select DepartmentId,JobTitle from employee where DepartmentId IN (SELECT DepartmentId from Departments);

Result

output 14

Query 15) To union the department name from departments table and firstname from employee:
Solution:

select departmentname from departments union select firstname from employee;

Result

output 15

Query 16) Rank employees by salary within each department:
Solution:
select EmployeeID,department,salary, rank() over(partition by department order by salary desc) as "Rank" from employee1;

Result
1

Query 17) Find the percentage contribution of each employee's salary within their department:
Solution:
SELECT EmployeeID, Name, Department, Salary, Salary * 100.0 / SUM(Salary) OVER (PARTITION BY Department) AS "PercentageContribution" FROM Employee1;

Result

2

Query 18) Calculate a running total of revenue for each customer:
Solution: SELECT customerID, OrderID, OrderDate, SUM(TotalAmount) OVER (PARTITION BY customerID ORDER BY OrderDate) AS "RunningTotal" FROM orders;

Result

3

Connect with me
🌐 GitHub Profile

📧 Email:shubhamkashyap9501@gmail.com

LinkedIn: Linkedin_link
