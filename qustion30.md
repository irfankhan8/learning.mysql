   ## 1. Name of all students jinhone abi tak koi fees deposit ni ki
   ```
    select * from student where id  not in(select distinct id from fees );
   ``` 

  ## 2. Sbse jyada fees kis student ne di hai. naam btao
  ```
   select sum(amount) as max,name from fees f join student s
   on s.id = f.id group by name order by max desc  limit 1 ;
  ``` 
   
 ## 3. Sbse jyada fees me 2nd number pr jo student hai uska naam btao 
 ```
   select name student, max(amount)as secmax , name from student s join fees f 
   on s.id = f.id group by name order by secmax desc limit 1,1;
```   
 ## 4. Coaching me total kitne employees hain unka naam and designation/role show krvao
 ```
    select count(id) from employee;
    select  emp_name ,employee  from employee e join employee_type t on 
    e.id = t.id group by emp_name ,id,emp_type;   
 ```   
 ## 5.Kis employee ne kitni salary uthayi hai ab tak vo btao ya month wise
 ```
   select sum(amount)as totel,name from salary s join 
   employe e on s.id = e.id group by name ;
 ```  
 ## 6.Vo sare students jo abi tak 1 b test me fail hue hai unka naam, subject, totalmarks, passingmarks, obtainedmarks btao
 ```
   select student.name , test.test_name,
   test.total_marks, test.passing_marks,result.obtainedmarks,
   result.result from student  join result  on student.id = result.id 
   join test  on test.id = result.id where result = 'fail';  
 ```  
 ## 7. Particular month ka kharcha btao. Kharche me tume salary and expenses dono add krne hai 
 ```
 
  
 ```
 ## 8. Particular month me total income btao 
 ```
   select  sum(amount) from fees where depositDate between '2022-01-01' and '2022-01-01';
```
 ## 9. Total income aaj tak 
 ```
       select sum(amount) from fees;
 ```      
## 10. Total kharche aaj tak 
```
  select sum(amount) from expenses;
```  
## 11. Kis course me kitne students hai vo btane hai 
```
  coursename startdate time totalstudents
  SELECT  c.course_name, c.startDate, c.timing, COUNT(sc.id) FROM   
           student s JOIN student_course sc ON s.stuId = sc.stuId      
           JOIN   course c ON c.id = sc.id  WHERE  
           sc.id IN (SELECT   id   FROM   course   WHERE   course_name = 'Nodejs') 
  GROUP BY sc.id , c.course_name , c.startDate , c.timing ;
 ``` 
 ## 12. Vo course btana hai jisme sbse jyada income hui hai 
 ```
  select c.course_name,sum(amount)as total from course c 
   join fees f on c.courseid = f.feesid join student_course sc on
   sc.stu_courseid = c.courseid group by c.course_name order by total desc limit 1;
 ```
 ## 13. Vo course btana hai jisme sbse kam income hui hai 
 ```
  select c.course_name, sum(amount)as total from course c join
  fees f on c.courseid = f.feesid group by course_name 
  order by total limit 1;
 
 ```
 ## 14. Kaunsa course hai jisme sbse jyada students hai 
  ```
    select  c.course_name as coursename , count(sc.stuId) as stuCount from course c join 
    student_course sc on  c.courseId = sc.courseId group by c.course_name limit 1 ;
  ```  
 ## 15. Kaunsa course hai jisme sbse kam students hain
 ```
   select  c.course_name,count (s.studentid) as total from student s 
   join course c on s.studentid = c.courseid join student_course sc on
 
  sc.stu_courseid = s.studentid group by course_name order by total limit 1; ??

```
 
 
  ##  1. Kaunsa course hai jisme koi admission ni hua hai
  ```    
    select * from course where courseId not in (select courseId from student_course )
 ```
  ##  2. Sbse jyada expense from expense table kis chiz ke liye hua hai 
 ```
    select amount , exp_detail from expenses where amount =( select max(amount) from expenses)
 ```
    
 ## 3. Employee list print krvani hai unki total paid salary ke descending order me
   * Sajid Teacher 100000
   * Shahrukh Teacher 80000
   * Rehna Peon 20000
 ```
    select e.emp_name ,sum(s.amount) from employee e join salary s on 
    e.employeeid = s.salaryid group by emp_name,s.amount order by amount  desc;
 ```
 ## 4. Course table ko alter krna hai aur usme ek teacherid column add krna hai jo ki foreign key hogi 
 ```
      alter table course add column teacherid int;
      alter table course add foreign key (teacherid) references employee(employeeid)
 ```     

  ## 5. Kaunse course me kaunsa teacher pdhata hai uski detail print krvani hai CourseName CourseTime TeacherName
  ```
     select c.course_name, c.timing,e.emp_name from course c join employee e on
     c.courseid = e.employeeid;
 ```

  ## 6. Student list print krvani hai unki total paid fees ke descending order me
   *    Sajid Nodejs 100000
   *    Shahrukh JavaScript 80000
   *    Rehna HTML 20000
  ```
    select s.name ,sum(f.amount) from student s join fees f on s.studentid = f.feesid 
    group by s.name , f.amount order by  amount desc;
 ```
 
  ## 7. Kisi b year ka total profit/loss btana hai
  ```
     Total fees - (total salary + total expenses)
     select ((select  sum(amount)as total from fees)
   - (select sum(amount)as total from  salary) + (select sum(amount)as total from expenses) )
```
  ## 8. Student count list print krvani hai unki total batch count ke descending order me
   *  Nodejs 10:00PM 10/01/2023  10/07/2023 30
   *  JS 9:00PM 10/01/2023  10/07/2023 20
   *  HTML 10:00AM 10/01/2023  10/07/2023 40
   ```
     select c.course_name , c.startDate, c.endDate , c.timing , count(sc.stuId) 
     from course c join student_course sc on c.courseId = sc.courseId 
     group by c.course_name , c.startDate, c.endDate , c.timing ;
   ```  

## 9. Student list print krvani hai unki total student in pincode ke descending order me
 *   302012 Jhotwara 20
 *   303012 Merta 15
 *   304013 Sikar 12 
 ```
   select pincode ,city,count(*) from address group by city , pincode;
 ```

## 10. Ek view bnana hai. 
 * StudentName Mobie Email CourserName CourseStartDate CourseEndDate Time TotalFees AvgMarks Address(plotno, colony, city, state, pincode)
```
 create view studentview(
  name , mobile , email,coursename , startDate , endDate , timing , totalamount , avgmarks , city , pincode)  as 
  select s.name , s.mobile ,s.email , c.course_name , c.startDate , c.endDate ,
  c.timing ,sum(f.amount), avg(r.obtainedmarks) , ad.city , ad.pincode
  from  result r  join address ad  on r.stuId = ad.stuId join  fees f  on ad.stuId = f.stuId join 
  student s on f.stuId = s.stuId join  student_course sc  on s.stuId = sc.stuId  join course c  on sc.courseId = c.courseId  
  group by 
  s.name , s.mobile ,s.email , c.course_name , c.startDate , c.endDate ,
  c.timing  , ad.city , ad.pincode;  //?
```

  ##  11. Ek view result pr bnana hai 
  ```
    StudentName Mobile TotalMakrs TotalOBtainedMarks Avg Rank
    Sajid 945655445 500 400 80 1
 ```

## 12. Vo student jinhone koi b fees jama ni krayi hai unko delete kr dena hai student table se 
 Aur iske child records Address, Result tables me hai vo vha se b delete krna hai 
```
 set sql_safe_updates =0;
 set froign_key_checks =0;
 delete from student where studentid not in (select studentid from fees);
 set froign_key_checks = 1;


```

## 13. Expenses table se monthly expenses descending order me btane hai 
 *  Year Month TotalExpenses
 *  2023 Feb 25000
 *  2022 Dec 12000
```
    select year (expenses.date)as year,month (expenses.date)as month,
    sum(amount)as totak from expenses group by year,month;
```

## 14. Kaunse teacher ke batch ke students ki performance sbse best hai 
```
  select e.name as teachername ,s.studentname,c.course_name,avg(r.obtainedmarks)as marks
  from course c join exmpoyee e on c.teachherid = e.employeeid join student_course sc on
  sc.stu_courseid join student s on s.studentid =sc.studentid
  join result r on r.resultid = s.studentid
  group by teachername, s.tudentname, c.course_name order by marks desc limit 1;


```
## 15. ek view bnana hai 
TeacherName BatchName BatchStartDate BatchEndDate Designation TotalFeesDepositByThisBatch  TotalSalary
```
 create view teacherecord as 
 select e.name, c.coursename,c.starDate, c.endDate,e.work,sum(f.amount)as this_batch,
 sum(sa.amount)as total_salary from employee e join course c on c.teacherid = e.employeeid
 join student_course sc on sc.courseid = sc.studetid
 join salary sa on sa.employeetypeid = e.employeeid 
 group by e.name, c.oursename, c.starDate , c.endDate,e.work ;



```
