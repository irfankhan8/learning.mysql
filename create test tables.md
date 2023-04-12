
   
   ## MYSQL 
   
   ```
   ````
   ## Create database
   ```
      create database institute_management
   ```
   
  ## Create Student table
  ```
    create  table Student(
        stuid          int unsigned primary key not null auto_increment,
        Name           varchar(155),
        FatherName     varchar(155),
        Mobile         int(10),
        Email          varchar(155),
        Address        varchar(155),
        AdmissionDate  varchar(255)
       
        );

```
  ##    Create table Employee
  ```
    create table Employee(
        Employeeid        int unsigned primary key not null auto_increment,
        Name              varchar(155),
        EmployeeTyepid    int  unsigned,
        constraint         Fk_Resulte_EmployeType foreign key(Employeeid)
        references         Student(stuid)
        )
  ```
  ##  Create table EmployeeType
  ```
        create table EmployeeType(
        Employeeid     int unsigned primary key not null auto_increment,
        EmployeeType	 varchar(155)
        
        )

 ```
   ##  Create table Course
   ```
    create table Course(
        courseid         int unsigned primary key not null auto_increment,
        Subject          varchar(155) not null,
        subFees      	   int not null,
        starDate         date not null,
        EndDate          date not null,
        Time             time not null,
        courid           int unsigned,
        constraint Fk_Result_courid foreign key(courid)
        references  Student(stuid)
         );

   ```
   
            
   ## Create table studentCourse
   ```
           create table studentCourse(
            Studentcourseid    integer unsigned primary key not null auto_increment,
            stuid              integer not null,
            Courseid           integer not null
            )

  ```
  ##  Create table Fees
  ```
            create table Fees(
            Feesid        int unsigned primary key not null auto_increment,
            Amount        bigint not null,
            Month         varchar(155),
            Fedid         int unsigned,
            constraint FK_Result_Feesid foreign key (Feesid)
            references Student(Stuid)
            )

 ```
 ## Create table stuTest
 ```
        create table stuTest (
            Testid       int unsigned primary key not null auto_increment,
            Name         varchar(155) not null,
            passingmark  int not null,
            totalmark    int not null,
            tastdate     date,
            teid         int  unsigned,
            constraint Fk_Resulet_Testid foreign key(teid)
            references   Student(stuid)
            
            )
    
 ```   
 ## Create table Result
 ```
        CREATE TABLE Result (
            Resulid       INT UNSIGNED PRIMARY KEY NOT NULL AUTO_INCREMENT,
            Totalmark     INT NOT NULL,
            ObtainedMark  INT NOT NULL,
            ResultPandF   VARCHAR(155) NOT NULL,
            stuid         INT NOT NULL,
            Testid        INT NOT NULL
           
        );
 ```
 ## Create table salary
 ```   
    CREATE TABLE Salary(
            Salaryid     INT UNSIGNED PRIMARY KEY NOT NULL AUTO_INCREMENT,
            Employeeid   INT NOT NULL,
            Amount       BIGINT NOT NULL,
            Month        VARCHAR(155),
            Salarid      INT UNSIGNED,
            CONSTRAINT Fk_Result_Salaryid FOREIGN KEY (Salarid)
                REFERENCES Employee(Employeeid)
        );

```
## Create table Exenses
```
        create table Expenses(
            Expensesid    int unsigned primary key not null auto_increment,
            ExpenDetails  varchar(155) not null,
            Amount        bigint not null,
            Date          date 
            )
