##  1.What is the query to get all the details of a student along with the fees and result data for the student ?
   ```
     select * from students p inner join fees q
     on p.Studentid = q.Sfid
     inner join Result f
     on f.Studentid = p.Studentid;
  ```
##  2.How can we retrieve the data of a student who has paid fees for the month of January ?
   ```
      select * from students f inner join fees q
      on f.Studentid = q. Sfid where Month = 'jan'
   ```      
##  3.What is the query to get the list of all students who have not yet paid their fees ?
   ```
     select * from students f inner join fees q
     on f.Studentid =  q.Sfid where Amount is null and Month is null;
  ```     

## 4.How can we fetch the list of students who scored more than 80 marks in any subject in the result table ?
   ```
     select * from students f inner join Result q 
     on  f.Studentid  = q.Studentid where Obtainedmarks >80
  ```     
## 5.What is the query to get the details of students along with the total amount of fees they have paid so far ?
  ```
     select Studentid, students.name,students.Studentid,sum(fees.Amount)as total from students
     left join fees on Studentid = fees.Sfid group by  Studentid
  ```    
## 6.How can we fetch the list of all students along with their fees data and result data, even if they do not have any data in the fees or result table ?
  ```
   select * from students f join Result q
   on f.Studentid = q.Studentid
   join fees p on p.Sfid = f.Studentid
  ```     
## 7.What is the query to get the name, email address, and mobile number of all the students who belong to the city of "Delhi" ?
  ```
     select s.Name, s.Pincode, Mobile from students s
     where s.City  like 'Marta%'
            
  ```      

## 8.How can we retrieve the details of students who belong to the city of "Mumbai" and have paid their fees for the month of February ?
  ```
      select * from students f 
      join fees s  on f.Studentid = s.Sfid 
      where f.City = 'Marta City' and s.Month = 'jan' 
   ```        
            
## 9.What is the query to get the name, email address, and total amount of fees paid by all the students who have paid their fees ?
   ```
                select Name,mobile, sum(Amount)as total from 
                students f join fees s on f.Studentid = s.Sfid
                group by Name, mobile
  ```      
## 10.How can we fetch the details of all students who have taken any test before a specific date   ?
  ```
                 select * from students f join Result s
                 on f.Studentid = s.Studentid
                where Testdate < 1991;
                
 ```      
 
  
## 11.What is the query to get the name, email address, and subject name of all the students who have scored more than 90 marks in any subject?
  ``` 
    select s.Name, s.Mobile Subject,f.Obtainedmarks from  students s join 
    Result f on s.Studentid  = f.Studentid where  f.Obtainedmarks >90
``` 
## 12.How can we retrieve the details of students who belong to the city of "Bangalore" and have scored less than 50 marks in any subject?
  ```
    select * from students f join 
    Result q on f.Studentid = q.Studentid
    where q.Obtainedmarks < 50 and f.City = 'Marta City'
 ```  
## 13What is the query to get the details of all students along with their fees and result data, sorted by their name in ascending order?
  ```
    select * from students f join fees q 
    on f.Studentid  = q.Sfid  join Result s 
    on  f.Studentid  = s.Studentid 
    order by f.Name asc;
 ```  
## 14How can we fetch the name, email address, and total amount of fees paid by all the students who have not paid their fees yet?
  ```
    select s.Name,s.mobile, coalesce(sum(f.Amount),0)as total 
    from students s left join fees f on s.Studentid = f.Sfid
    where f.Amount is null 
    group by s.Studentid;
```   
## 15What is the query to get the details of all students who have paid their fees for the month of March and have scored more than 70 marks in any subject?
   ```
     select * from students s join fees f
     on s.Studentid = f.Sfid join Result r 
     where  f.Amount is not null 
     and f.Month = 'March'
     and r.Obtainedmarks >70 
 ```    
## 16How can we retrieve the details of students who have not taken any test yet?
   ```
     select * from students s left join 
     Result r on s.studentid = r.Studentid
     where r.Subject is null
 ```    
## 17What is the query to get the name, email address, and subject name of all the students who have scored less than 40 marks in any subject?
   ```
     select s.Name,s.Pincode, r.Subject from students s join fees f 
     on s.Studentid = f.Sfid  join Result r 
     on r.Studentid = s.Studentid
     where r.Obtainedmarks >70;
  ```   
## 18How can we fetch the details of students who belong to the city of "Pune" and have paid their fees for the month of January?
   ```
      select * from students s inner join fees f 
      on s.Studentid = f.Sfid join Result r 
      on r.Studentid = s.Studentid
      where s.City like  'Marta%'
      and f.Month  = 'jan'
      and f.Amount is not null;
 ```     
## 19What is the query to get the name, email address, and mobile number of all the students who have not taken any test yet?
   ```
       select s.Name, s.Pincode , s.Mobile  from students s left join 
       Result r on s.Studentid = r.Studentid
       where r.Subject is null
 ```      
## 20How can we retrieve the details of students who have scored more than 60 marks in all the subjects they have taken tests for? 
   ```
     select * from students s join Result r
     where r.Obtainedmarks > 60
  ```      
 
