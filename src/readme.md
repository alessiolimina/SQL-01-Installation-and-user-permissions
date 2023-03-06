Exercise - SQL-installation-and-user-permissions
install MySQL on your computer following this tutorial by:
creating an Oracle account (first step necessary to download the necessary files)
downloading MySQL installer web community
launch the setup wizard:
choose Developer Default as setup type (it will take some time to download and install all the necessary files)
leave all the default options for Type and Networking and for Authentication Method
create a Root Account:
you have to create - and remember! - a MySQL Root Password
create 1 admin user:
username admin, host: All hosts, role DB Admin and assign (and remember!) a password
leave all the default options for the Windows Service
finalise the application by applying the configuration
leave all the default options for MySQL Router Configuration
connect to the MySQL Server by entering your root password for receiving sample schemas and data
at the end of the setup wizard, launch only MySQL Shell
[Optional] if the shell opens with MySQL JS, switch to SQL using the command \sql
using MySQL Shell:
connect using your root account: \connect root@localhost
create 3 users:
create a developer user: CREATE USER 'developer'@'localhost' IDENTIFIED BY 'passwordhere';
after each user-related command it's recommended to execute this command: FLUSH PRIVILEGES;
create a viewer user: CREATE user 'viewer'@'localhost' IDENTIFIED BY 'passwordhere';
create a writer user: CREATE user 'writer'@'localhost' IDENTIFIED BY 'passwordhere';
verify that all the users have been created (the 3 new ones + root and admin created during the setup):
SELECT User from mysql.user;
create 3 roles (app_developer, app_read and app_write):
CREATE ROLE 'app_developer', 'app_read', 'app_write';
assign privileges to the roles:
GRANT ALL ON *.* TO 'app_developer';
GRANT SELECT ON *.* TO 'app_read';
GRANT INSERT, UPDATE, DELETE ON *.* TO 'app_write';
assign the roles to the users:
GRANT 'app_developer' TO 'developer'@'localhost';
GRANT 'app_read' TO 'viewer'@'localhost';
GRANT 'app_write' TO 'writer'@'localhost';
you can read more about user creation, roles and privileges here
create a new database called newdb
CREATE DATABASE IF NOT EXISTS newdb;
assign privileges to the 3 users:
GRANT ALL PRIVILEGES ON newdb . * TO 'developer'@'localhost';
GRANT SELECT ON newdb.* TO 'viewer'@'localhost';
GRANT INSERT, UPDATE, DELETE ON newdb.* TO 'writer'@'localhost';