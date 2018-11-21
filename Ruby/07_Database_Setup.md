Ruby on Rails - Database Setup
Advertisements
 Previous Page Next Page  
Before starting with this chapter, make sure your database server is up and running. Ruby on Rails recommends to create three databases - a database each for development, testing, and production environment. According to convention, their names should be −

library_development
library_production
library_test
You should initialize all three of them and create a user and password for them with full read and write privileges. We are using the root user ID for our application.

Database Setup for MySQL
In MySQL, we are using the root user ID for our application. The MySQL console session in which you do this looks something like −

mysql> create database library_development;
Query OK, 1 row affected (0.01 sec)

mysql> grant all privileges on library_development.*
to 'root'@'localhost' identified by 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
You can do the same thing for two more databases library_production and library_test.

Configuring database.yml
At this point, you need to let Rails know about the user name and password for the databases. You do this in the file database.yml, available in the library\config subdirectory of Rails Application you created. This file has live configuration sections for MySQL databases. In each of the sections you use, you need to change the username and password lines to reflect the permissions on the databases you've created.

When you finish, it should look something like −

development:
   adapter: mysql
   database: library_development
   username: root
   password: [password]
   host: localhost
	
test:
   adapter: mysql
   database: library_test
   username: root
   password: [password]
   host: localhost
   
production:
   adapter: mysql
   database: library_production
   username: root
   password: [password]
   host: localhost
Database Setup for PostgreSQL
By default, PostgreSQL does not provide any users. We have to create new users. Use the following command to create a user with the name rubyuser.

tp> sudo -u postgres createuser rubyuser -s
If you want to create a password for the new user, then use the following command.

tp> sudo -u postgres psql

postgres=# \password rubyuser
Use the following command for creating a database library_development.

postgres=# CREATE DATABASE library_development OWNER rubyuser; 

CREATE DATABASE
Use the following command for creating a database library_production.

postgres=# CREATE DATABASE library_production OWNER rubyuser; 

CREATE DATABASE
Use the following command for creating a database library_test.

postgres=# CREATE DATABASE library_test OWNER rubyuser; 

CREATE DATABASE
Press Ctrl+D to terminate PosgreSQL.

Configuring database.yml
At this point, you need to let Rails know the username and password for the databases. You do this in the file database.yml, available in the library\config subdirectory of Rails Application you created. This file has live configuration sections for PostgreSQL databases. In each of the sections, you need to change the username and password lines to reflect the permissions on the databases you've created.

When you finish, it should look as follows −

default: &default
   adapter: postgresql
   encoding: unicode
  
development:
   adapter: postgresql
   encoding: unicode
   database: library_development
   username: rubyuser
   password: <Password for rubyuser>

test:
   adapter: postgresql
   encoding: unicode
   database: library_test
   username: rubyuser
   password: <Password for rubyuser>
 
production:
   adapter: postgresql
   encoding: unicode
   database: library_production
   username: rubyuser
   password: <Password for rubyuser>
What is Next?
The next two chapters explain how to model your database tables and how to manage those using Rails Migrations.