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

### Configure login & security standards and Launch the database Server:

```bash
sudo mysql_secure_installation 
sudo mysql
```
### While DB Server is launched, create user and grant previleges: 
```bash
CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY 'Password.11';
CREATE DATABASE test_db;
GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
### In server, show database:
```bash
Show databases;
```
![client DB](https://github.com/macdonaldojong/PBL5_CLIENT-SERVER-ARCHITECTURE-USING-A-MYSQL-RELATIONAL-DATABASE-MANAGEMENT-SYSTEM/blob/037d48d5b4a7af69d601d59262012149bbc6c2d1/image/Server%20DB.PNG)
## Now in mysql-client machine,
### Mysql/Aurora uses TCP Port 3306 by default.
### Create a new rule in the {client's security group}, allowing connections on port:3306 to client permitted only through {server's_private_ip} address.

![change config file for server](https://github.com/macdonaldojong/PBL5_CLIENT-SERVER-ARCHITECTURE-USING-A-MYSQL-RELATIONAL-DATABASE-MANAGEMENT-SYSTEM/blob/037d48d5b4a7af69d601d59262012149bbc6c2d1/image/client%20security%20group%20configuration%20to%20accept%20server%20ip.PNG)

### Configure MySQL server to allow connections from remote hosts by
### Locate the bind address and Replace ‘127.0.0.1’ to ‘0.0.0.0’
```bash
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

![change config file for server](https://github.com/macdonaldojong/darey_project5/blob/a12f5415de4a44f0219c56046ddbf1a3bed00369/image/change%20config%20file%20for%20server.PNG)

### From mysql client Linux Server connect remotely to mysql server Database Engine without using SSH
```bash
sudo mysql -u remote_user -h 172.31.12.125 -p # where this 172.31.12.125 is {server's_private_ip}
Show databases;
```
![client DB](https://github.com/macdonaldojong/darey_project5/blob/a12f5415de4a44f0219c56046ddbf1a3bed00369/image/client%20DB.PNG)
