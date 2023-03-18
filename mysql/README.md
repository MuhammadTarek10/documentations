# Installing MySql
```
brew install mysql
```
# Starting MySql
```
mysql.server start
```
# Stopping MySql
```
mysql.server stop
```
# Creating a database
```
mysql -u root -p
```
```
create database <database_name>;
```
# Creating a user
```
create user <user_name> identified by '<password>';
```
# Starting shell
```
mysql -u <user_name> -p
```