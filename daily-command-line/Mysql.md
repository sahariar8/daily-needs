### How to enter mariadb docker container from local machine
```
  mysql -h 127.0.0.1 -P 3307 -u root -p
```

### How to enter local machine mysql
```
  mysql -h 127.0.0.1 -P 3306 -u root -p
  or
  mysql -u root -p
```

### How to install mariadb using docker and port 3307
```
  docker run -d --restart always -p 3307:3306 --name mariadb-container -e MYSQL_ROOT_PASSWORD=your_root_password mariadb:10.8
```
### Install MariaDB in Ubuntu
  ```
    sudo apt update
  ```
### Install the MariaDB server package
  ```
    sudo apt install mariadb-server
  ```
### Once the installation is complete, you can start the MariaDB service:
  ```
    sudo systemctl start mariadb
  ```
### You might also want to enable the MariaDB service to start on boot:
 ```
  sudo systemctl enable mariadb
 ```
### You can verify that MariaDB has been installed and is running correctly by checking its status:
  ```
    sudo systemctl status mariadb
  ```
### Additionally, you can access the MariaDB shell to interact with the database:
  ```
    sudo mariadb
  ```
## How to set password for the root user in MariaDB.
### First, ensure that the MariaDB service is running. If it's not already running, start it using:
    ```
    sudo systemctl start mariadb
    ```
### Then, run the mysql_secure_installation script:
  ```
    sudo mysql_secure_installation
  ```

### How to show mysql port in locally
  ```
    mysql> SHOW VARIABLES LIKE 'port';
    or
    install netstat
    sudo apt install net-tools
    netstat -an | grep 3306

    or
    netstat -an | grep -w 3307

  ```

### How to install dbeaver in Ubuntu 22.04 LTS
[How to install dbeaver in Ubuntu 22.04 LTS](https://dbeaver.io/download/)

```
sudo snap install dbeaver-ce
```
### How to install MySQL in Ubuntu 22.04 LTS 
[How to install MySQL in Ubuntu 22.04 LTS Documentation](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04)

-1st update the package
  ```
  sudo apt update
  ```
-2nd install the mysql-server package
  ```
  sudo apt install mysql-server
  ```
-3rd Ensure that the server is running using the systemctl start command:
  ```
  sudo systemctl start mysql.service
  ```
-4th open up the MySQL prompt:
  ```
  sudo mysql
  ```
-5th Then run the following ALTER USER command to change the root user’s authentication method to one that uses a password. The following example changes the authentication method to
 ```
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
 ```
-6th After making this change, exit the MySQL prompt:
  ```
  exit
  ```
-7th Run the security script with sudo:
  ```
  sudo mysql_secure_installation
  ```
-8th To authenticate as the root MySQL user using a password, run this command:
  ```
  mysql -u root -p
  ```

### How to check MySQL and MariaDB Version
```
mysql -V
mariadb -V
```
### Restoring a MySQL Database using command line:
  - 1st step: 
    - Open a Terminal:
        ```Open a terminal or command prompt on your system.
        ```
  - 2nd step:
    - Navigate to the Directory Containing the Backup and Use the cd command to navigate to the directory where your backup file is located. For :
        ```shell
            cd /path/to/backup/directory
        ```
  - 3rd step:
    - Use mysql Command, Use the mysql command along with the appropriate options to restore the database::
        ``` shell
              mysql -u username -p database_name < backup_file.sql
        ```
    - Replace username with your MySQL username.
    - Replace database_name with the name of the database you want to restore.
    - Replace backup_file.sql with the name of your backup file.
      
###  How to Backup MySQL DB using command line

  - 1st step: 
    - Open a Terminal:
        ```Open a terminal or command prompt on your system.
        ```
  - 2nd step:
    - Use mysqldump Command and Use the mysqldump command followed by the database name to create a backup:
        ```shell
            mysqldump -u username -p database_name > backup_file.sql
        ```
    - Replace username with your MySQL username.
    - Replace database_name with the name of the database you want to back up.
    - backup_file.sql is the name of the file where the backup will be saved.


### How to enter inside mysql server in command line.
```
mysql -u (username) -p (password)
```
### How to connect database
```
use database_name;
```
### How to show all tables
```
show tables;
```
### How to Check the Status of mysql Service?
```
sudo systemctl status mysql
```
### How to restart MariaDB
```
sudo systemctl restart mariadb
```
### How to show database Log File in Docker mariadb
- First Execute this line to check its working or not for docker database DB
```
  SET GLOBAL general_log = 'ON';
  SET GLOBAL general_log_file = '/var/log/mysql/sql_log1.log';
```
- Secondly enter a mariadb database container using this command
```
docker exec -it (container id) bash
```
- Thirdly enter this location
```
root@a3f371b6277c:/var/log/mysql#
```
- Fourthly create file using this command
```
touch sql_log1.log (your log file name)
```
- Fifth show this file using this command
```
cat sql_log1.log (your log file name)
```
- Delete all data from log file using this command
```
echo "" > /var/log/mysql/sql_log1.log
```
