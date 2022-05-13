## IMPLEMENT: A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS)

## Step1 - Setup two instances of mysql in AWS:

##- mysql server
### change name on Ubuntu -> mysql-server
* sudo nano /etc/hostname
* sudo reboot
##- mysql client
### change name on Ubuntu -> mysql-client
* sudo nano /etc/hostname
* sudo reboot

## Update & upgrade both instances
* sudo apt update -y
* sudo apt upgrade -y

## Step2 -Install mysql-server software on mysql-server machine // Install mysql-client on client machine
### mysql-server machine
sudo apt install mysql-server -y
sudo systemctl start mysql

### mysql-client machine
sudo apt install mysql-client -y
sudo systemctl start mysql

### Mysql server uses TCP Port 3306 by default.
### Create a new rule in the client security group, allowing connections on port 3306 to client only through server private ip address.
### Launch the DB Server

```bash
sudo mysql_secure_installation 
sudo mysql
```
### Allow client private ip address in the inbound rules while selecting mysql
### Run this script on mysql-Server machine
```bash
CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'Password.11';
CREATE DATABASE test_db;
GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
### Configure MySQL server to allow connections from remote hosts
```bash
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
### Locate the bind address and Replace ‘127.0.0.1’ to ‘0.0.0.0’

![change config file for server](https://github.com/macdonaldojong/darey_project5/blob/a12f5415de4a44f0219c56046ddbf1a3bed00369/image/change%20config%20file%20for%20server.PNG)

### From mysql client Linux Server connect remotely to mysql server Database Engine without using SSH
```bash
sudo mysql -u remote_user -h 172.31.12.125 (private ip of mysql-server) -p
Show databases;
```
![client DB](https://github.com/macdonaldojong/darey_project5/blob/a12f5415de4a44f0219c56046ddbf1a3bed00369/image/client%20DB.PNG)
