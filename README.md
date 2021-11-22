# RDAddrBook
Simple addressbook with MariaDB back-end

## Install Java 1.8
```
yum -y install java-1.8.0-openjdk
```

## Install Maven
```
yum -y install maven
```

## Install MariaDB
```
yum -y install mariadb mariadb-server
systemctl start mariadb
systemctl enable mariadb
```

### Secure MariaDB
```
sudo mysql_secure_installation
```
> Enter 'root' password

## Setup application database
```
mysql -u root -p
```
> Enter 'root' password
### Create application database
```
create database rdaddrbook;
```
### Create application user
```
create user addrbook@localhost identified by 'rdaddrbook';
create user addrbook@'10.0.0.132' identified by 'rdaddrbook';
```
### Grant privileges on application database
```
grant all privileges on rdaddrbook.* to addrbook@'%' identified by 'rdaddrbook';
grant all privileges on rdaddrbook.* to addrbook@'localhost' identified by 'rdaddrbook';
```

## Get Application Source Code
- Clone from this Repo

## Application Configuration
### Database Hostname
- Update Database Hostname depending on your environment
- File: src/main/resources/application.properties
### Database credentials
- Update Database username, password
- File: src/main/resources/application.properties

## Build Application
- Use Maven Command:
```
cd RDAddrBook
mvn -DskipTests clean install
```

## Run Application
- Start application
```
cd RDAddrBook
java -jar target/RDAddrBook-0.0.1-SNAPSHOT.jar
```

## Verification
### Create a Contact resource
```
curl "http://ec2-18-183-105-92.ap-northeast-1.compute.amazonaws.com:9080/api/contacts" \
  -X POST \
  -d "{\n  \"firstName\": \"Ganesh\",\n  \"lastName\": \"Sharma\",\n  \"groupName\": \"Friends\",\n  \"organization\": \"IBM\",\n  \"job\": \"Architect\",\n  \"notes\": \"some notes\"\n}" \
  -H "content-type: application/json" 
```
### Get all Contact resources
```
curl "http://ec2-18-183-105-92.ap-northeast-1.compute.amazonaws.com:9080/api/contacts"
```

