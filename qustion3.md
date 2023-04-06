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
                where Testdate > 1991;
                
 ```      
