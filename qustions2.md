## How many students are there in the student table?
   ---
     select count(*) from student;
  ---
## What is the name of the student with studentid = 5?
  ---
    select name from student where studentid  = 5;
---
## How many students are there from the city of Mumbai?
  ---
    select count(*) from student where city  = 'Mumbai';
---
## What is the email address of the student whose name is 'John Doe'?
  ---
    select email_address from student where name  = 'John Doe';
---
## What is the total amount of fees paid by the student with studentid = 10?
   ---
     select sum(amount) from fee where studentid  = 10;
  ---
## What is the highest amount of fees paid by any student?
  ---
    select max(amount) from fee;
---
 ## What is the average amount of fees paid by all students?
  ---
    select avg(amount) from fee;
---
## What is the name of the student who paid the highest amount of fees?
  ---
    select studentid, max(amount) as maxamount from fee;
    select * from student where studentid  = ?
---    

## What is the total marks obtained by the student with studentid = 7?
   ---
     select sum(obtainedmarks) from result where studentid  = 7;
 ---
## What is the highest marks obtained by any student?
  ---
    select max(obtainedmarks) from result;
---
## What is the average marks obtained by all students?
  ---
    select avg(obtainedmarks) from result;
---
##  What is the name of the student who obtained the highest marks?
  ---
    select max(obtainedmarks), studentid from result;
    select * from student where studentid  = ?;
---
## What is the total amount of fees paid by all students from the city of Delhi?
  ---
    select studentid from student where city = 'Delhi';
    select sum(amount) from fee where studentid in (?,?);
---
##  What is the total amount of fees paid for the month of January?
   ---
     select sum(amount) from fee where month  = 'Jan';
 ---
## What is the total amount of fees paid by all students for the subject of mathematics?
  ---
    select studentid from student where course = 'Mathematics';
    select sum(amount) from fee where studentid in (?,?);
---
## What is the average marks obtained by the student with studentid = 9 for the subject of science?
   ---
     select avg(obtainedmarks) from result where studentid = 9 and subject = 'Science';
---
## What is the name of the student who paid the highest amount of fees for the month of February?
   ---
     select max(amount), studentid from fee where month  = 'Feb';
 ---
## What is the name of the student who obtained the highest marks in the subject of English?
  ---
    select max(obtainedmarks), studentid from result where subject  = 'English';
     select * from student where studentid = ?

---
## What is the name of the student who paid the highest amount of fees for the subject of computer science?
   ---
     select max(amount),studentid from fee where subject  = 'Computer Science';
      select * from student where studentid = ?
      
---      
