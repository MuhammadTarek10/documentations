# Installing MySql
```
brew install mysql
```
# Starting MySql
```
brew services start mysql
mysql.server start
```
# Stopping MySql
```
brew services stop mysql
mysql.server stop
```
# Creating a database
Note: password initially is ```root```
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
