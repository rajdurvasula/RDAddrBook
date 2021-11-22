# RDAddrBook
Simple addressbook with MariaDB back-end

## Install Java 1.8
yum -y install java-1.8.0-openjdk

## Install Maven
yum -y install maven

## Install MariaDB
yum -y install mariadb mariadb-server
systemctl start mariadb
systemctl enable mariadb

### Secure MariaDB
sudo mysql_secure_installation
> Enter 'root' password

## Setup application database
mysql -u root -p
> Enter 'root' password
### Create application database
create database rdaddrbook;
### Create application user
create user addrbook@localhost identified by 'rdaddrbook';
create user addrbook@'10.0.0.132' identified by 'rdaddrbook';
### Grant privileges on application database
grant all privileges on rdaddrbook.* to addrbook@'%' identified by 'rdaddrbook';
grant all privileges on rdaddrbook.* to addrbook@'localhost' identified by 'rdaddrbook';

