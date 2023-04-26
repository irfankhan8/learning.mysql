   ## 1. Name of all students jinhone abi tak koi fees deposit ni ki
   ```
    select * from student where studentid not in (select distinct feesid  from fees )
   ``` 

  ## 2. Sbse jyada fees kis student ne di hai. naam btao
  ```
    select name student, max(f.amount) as stumax from  student s join fees f 
    on s.studentid = f.feesid group by name order by stumax  desc limit 1
  ``` 
   
 ## 3. Sbse jyada fees me 2nd number pr jo student hai uska naam btao 
 ```
   select name student , max(f.amount) as secmax,name from student s join fees f
   on s.studentid = f.feesid group by name order by secmax  desc limit 1,1  
```   
 ## 4. Coaching me total kitne employees hain unka naam and designation/role show krvao
 ```
     select emp_name employee , count(e.employeeid) as coun from 
     employee e join employee_type et
     on e.employeeid = et.emp_typeid group by emp_name order by coun  desc;     
 ```   
 ## 5.Kis employee ne kitni salary uthayi hai ab tak vo btao ya month wise
 ```
   select e.employeeid,e.emp_name ,sum(amount)from employee e join salary s on 
   e.employeeid = salaryid group by employeeid ,emp_name
 ```  
 ## 6.Vo sare students jo abi tak 1 b test me fail hue hai unka naam, subject, totalmarks, passingmarks, obtainedmarks btao
 ```
   select s.studentid , s.name,t.test_name,t.total_marks,t.passing_marks,
    r.obtainedmarks from student s join result r on s.studentid =r.resultid
    join test t on s.studentid = t.testid and t.passing_marks > r.obtainedmarks
    group by s.studentid ,s.name,t.test_name,t.total_marks,t.passing_marks,
    r.obtainedmarks;  
 ```  
 ## 7. Particular month ka kharcha btao. Kharche me tume salary and expenses dono add krne hai 
 ```
   select (select sum(amount)from salary where date(date)='2023-03-20')+
   (select sum(amount)from expenses where date(expense_date)='2023-01-03')as total
 
 ```
 ## 8. Particular month me total income btao 
 ```
   select sum(amount) from fees where date(depositDate) ='2022-01-01' 
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
    select c.courseid,c.course_name,c.startDate,c.timing,count(c.courseid) from
    course c  join student_course st on
    c.courseid = st.stu_courseid group by c.courseid ,c.course_name,c.startDate,c.timing
 ``` 
 ## 12. Vo course btana hai jisme sbse jyada income hui hai 
 ```
  select c.course_name,sum(amount)as total from course c 
   join fees f on c.courseid = f.feesid join student_course sc on
   sc.stu_courseid = c.courseid group by c.course_name,c.courseid order by total desc limit 1;
 ```
 ## 13. Vo course btana hai jisme sbse kam income hui hai 
 ```
  select c.course_name, sum(amount)as total from course c join
  fees f on c.courseid = f.feesid group by course_name ,c.courseid
  order by total limit 1;
 
 ```
 ## 14. Kaunsa course hai jisme sbse jyada students hai 
  ```
    select  c.course_name as coursename , count(sc.stuId) as stuCount from course c join 
    student_course sc on  c.courseId = sc.courseId group by c.course_name,c.courseid limit 1 ;
  ```  
 ## 15. Kaunsa course hai jisme sbse kam students hain
 ```
   select  c.course_name,count (s.studentid) as total from student s 
   join course c on s.studentid = c.courseid join student_course sc on
 
  sc.stu_courseid = s.studentid group by course_name order by total limit 1; ??

```
 
 
  ##  1. Kaunsa course hai jisme koi admission ni hua hai
  ```    
    select  course_name from course where courseid not in (select distinct courseid from
      student_course);
 ```
  ##  2. Sbse jyada expense from expense table kis chiz ke liye hua hai 
 ```
    select exp_detail ,sum(amount)as expens from expenses 
    group by exp_detail order by expens desc limit 1;  
 ```
    
 ## 3. Employee list print krvani hai unki total paid salary ke descending order me
   * Sajid Teacher 100000
   * Shahrukh Teacher 80000
   * Rehna Peon 20000
 ```
    select e.employeeid,e.emp_name , sum(amount)as total from employee e left join salary s
    on e.employeeid = s.salaryid left join employee_type et on e.employeeid = et.emp_typeid
    group by e.employeeid,e.emp_name order by total desc; 
 ```
 ## 4. Course table ko alter krna hai aur usme ek teacherid column add krna hai jo ki foreign key hogi 
 ```
      alter table course add column teacherid int;
      alter table course add foreign key (teacherid) references employee(employeeid)
 ```     

  ## 5. Kaunse course me kaunsa teacher pdhata hai uski detail print krvani hai CourseName CourseTime TeacherName
  ```
     select  c.course_name, c.timing,e.emp_name from course c join employee e on
     c.courseid = e.employeeid;
 ```

  ## 6. Student list print krvani hai unki total paid fees ke descending order me
   *    Sajid Nodejs 100000
   *    Shahrukh JavaScript 80000
   *    Rehna HTML 20000
  ```
    select s.studentid,s.name ,c.course_name,sum(amount)as total from student s join
    fees f on s.studentid =f.feesid 
     join course c on c.courseid = f.feesid  group by s.studentid,s.name ,c.course_name
    order by total desc;    
 ```
 
  ## 7. Kisi b year ka total profit/loss btana hai
  ```
     select (select sum(amount)from fees where year(amount)=2023)-
    ((select sum(amount)from salary where year(amount)=2023)
  + (select sum(amount)from expenses where year (expense_date)=2023)) as total       
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
   select year (expense.date)as year,
   month(expenses.date) as month,sum(amount)
   as total from expenses group by year ,month order by total desc
```

## 14. Kaunse teacher ke batch ke students ki performance sbse best hai 
```
   select e.emp_name ,s.name,c.course_name,avg(r.obtainedmarks)as marks
      from course c join employee e on c.courseid = e.employeeid join student_course sc 
       join student s on s.studentid =sc.stu_courseid
       join result r on r.resultid = s.studentid
       group by e.emp_name,s.name, c.course_name order by marks desc limit 1;  


```
## 15. ek view bnana hai 
TeacherName BatchName BatchStartDate BatchEndDate Designation TotalFeesDepositByThisBatch  TotalSalary
```
   reate view teacherRecord as 
     select e.emp_name,c.course_name,c.startDate,c.endDate ,sum(f.amount)as batch, sum(sa.amount)as total
      from employee e join course c on e.employeeid = c.courseid join student_course sc on
      c.courseid = sc.stu_courseid join student s  on sc.stu_courseid = s.studentid join
       fees f on s.studentid = f.feesid join salary sa on e.employeeid = sa.salaryid 

       group by e.emp_name,c.course_name,c.startDate,c.endDate; 



```



## 1. Student ka count print krvana hai desc order me unke city ke according. for example
   *  totalstudents cityname
   *  25   Jaipur 
   *  20   agaur
   ```
     select city address, count(add_id) as citycount from 
     student s join address a
     on s.studentid = a.add_id group by city order by citycount  desc; 
  ```   

## 2. Kisi student ki sare months me kitni fees aayi hai vo btani hai sare months ki ab tak 
*  StudentName MonthName Fees 
* Sajid Feb, 2022 2000
* Sajid March, 2022 1000
* Sajid April 0
* Sajid May 1000
```
     select s.name ,f.depositDate , sum(f.amount)as manth   from student s join fees f
     on s.studentid = f.feesid group by  s.name , f.depositDate order by manth  desc;
     
*  Agar kisi month me koi fees ni aayi hai to 0 dhikana hai 
```
## 3. Kisi particular test me total kitne students pass fail hue hai vo btana hai 
* TestId TestName TotalPass TotalFail
* 1 Nodejs 10 5
* 2 JS 20 10
```
    select t.test_name ,r.result,count(r.result)as total from result r join test t on
   r.resultid = t.testid group by t.test_name,r.result  ;  ??
```   

## 4. Kisi particular month me total kitne test hue hai vo btane hai 
 * MonthName TotalTests
 * May 20
 * June 10
 ```
     select date(date)as date ,count(*) as total_tests from test where
       date(date) = '2023-01-16' group by date(date);

```
## 5. Kisi particular designation pr kitne employees hai vo btana hai 

 * Designation Count
 * Teacher    10
 * Peon 2
 * Receptionist 1
 ```
       select emp_name ,count(*) as count from employee where emp_name  ='techar'  
       group  by emp_name;
       select emp_name ,count(*) as count from employee where emp_name  ='pion'  
       group  by emp_name;
 ```      

## 6. Kisi particular designation ke employees ki total salary particular month me kitni hai vo btana hai 
* Designation Month TotalSalary
* Teacher June 25000
* Peon June 10000
* Receptionist June 5000
```
      select e.employeeid, et.emp_typeid,date(s.date),s.amount as total from employee e
       join salary s on e.employeeid = s.salaryid join 
         employee_type et on et.emp_typeid = e.employeeid group by e.employeeid,et.emp_typeid;
```       

## 7. Employees ki totalsalary ko desc order me btao with name 
   *  EmployeeName totalsalary
   *  Sajid  200000
   *  shahrukh 120000
   *  Raja 80000
  ```
       select e.employeeid , e.emp_name,sum(s.amount)as total from employee e 
        join salary s on e.employeeid = s.salaryid group by e.employeeid ,e.emp_name
        order by total desc;

  ```
## 8. Ek new table bnani hai jisme ye columns honge 
   *  TableName : TeacherSalaryRecord
   *  SalaryRecordId TeacherId(foreignkey)   TotalSalary 
  ```
      create table TeacherSalaryRecord(
       SalaryRecordid  int primary key auto_increment,
        Teacherid  int ,
         TotalSalary int not null,
          foreign key (Teacherid) references employee (employeeid)
            )
  ```          

##  9. Ek trigger bnana hai. Aur jab b salary table me kisi b employee ke liye entry hogito TeacherSalaryRecord table me uski totalsalary update hogi 

   *  Salary  : Sajid 10000
   *  TeacherSalaryRecord : Sajid 10000
   *  Salary Sajid 20000 
   *  TeacherSalaryRecord : Sajid 30000
   ```
     DELIMITER //
      CREATE TRIGGER salary_Aupt
      AFTER INSERT ON salary 
      FOR EACH ROW
      BEGIN
      UPDATE TeacherSalaryRecord SET Total = TotalSalary + NEW.amount WHERE TeacherId = NEW.employeeid;
       END;//  
 ```
## 10. Student table me studnetname, fathername pr index bnani hai  
```
 create index  index_stu on student (name,father_name)
  
``` 
