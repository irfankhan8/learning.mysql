 
## 1. khan
---
select * from student where name like '%khan%';
---
## 2. where studentid between 5 and 10
---
select * from student where studentid between 5 and 10;
---
## 3. Rename fathername column to mothername
---
ALTER TABLE student RENAME COLUMN fathername TO mothername;
---
### 4. kaunse month me sbse jyada fees aayi hai
---
select month, sum(amount) as total from fees group by month order by total desc limit 1;
---
### 5. kaunse month me sbse kam fees aayi hai
---
select month, sum(amount) as total from fees group by month order by total asc limit 1;
---
### 6. sbse jyada fees kis student ne di hai
---
select studentid, sum(amount) as total from fees group by studentid order by total desc limit 1;

select * from student where studentid = ?;
---
### 7. sbse kam fees kis student ne di hai
---
select studentid, sum(amount) as total from fees group by studentid order by total asc limit 1;

select * from student where studentid = ?;
---
### 8. aise kaunse student hai jinhone ek b bar fee ni di hai
---
select distinct studentid from fee;

select * from student where studentid not in (?, ?, ?);
---
### 9. aise kaunse students hai jinka mobile and fathername ni hai db me
---
select * from student where mobile is null and fathername is null;
---
### 10. vo sare students ka record delete krdo jinhone koi fees ni di hai
---
select distinct studentid from fee;

delete from student where studentid not in (?, ?, ?);
---
 
