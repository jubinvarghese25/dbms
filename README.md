create database abc;
use abc;
create table student(
RollNo int primary key,
Name varchar(100),
DOB date,
Department varchar(100)
);
insert into student(RollNo,Name,DOB,Department)
values
(101,'Raj','2005-02-02','Computer Science'),
(102,'Ram','2005-10-10','AIML'),
(104,'Rad','2006-12-12','Computer Science'),
(103,'Yash','2007-03-12','CSBS');
create table course(
CourseID int primary key,
Title varchar(100),
Credits varchar(2)
);
insert into course(CourseID,Title,Credits)
values
(201,'Database Management System',4),
(202,'Operating System',3),
(203,'Software Engineering',3),
(204,'Ethics',2);
create table enrollment(
RollNo int,
CourseId int,
Grade char(2),
primary key(RollNo,CourseID),
foreign key(RollNo)references student(RollNO),
foreign key(CourseID)references course(CourseID)
);
insert into enrollment(RollNo,CourseID,Grade)
values
(101,201,'A'),
(102,202,'B'),
(103,203,'C'),
(104,204,'B');

select count(*) as total_student from student;

select count(*) as total_student from course;

select avg(Credits) as average_credits from course;

select min(Credits) as min_credit,
max(Credits) as max_credit from course;

select RollNo,Name,Department from student
order by Name ASC;

select CourseID,Title,Credits from course
order by Credits desc;

select Department,count(*) as No_of_student from student
group by Department;

select C.Title as course_name,count(E.RollNo) as total_enrollment from course C
Join Enrollment E on C.CourseID=E.CourseID group by c.Title;

select Department,count(*) as student_count from student
group by Department
having count(RollNo)>0;

select C.Title as Course,count(E.RollNo) as Student_Enrolled,
avg(C.Credits) as Avg_credits from course C
Join Enrollment E on C.CourseID=E.CourseID 
group by C.Title
having count(E.RollNo)>=1
order by Student_Enrolled desc;
