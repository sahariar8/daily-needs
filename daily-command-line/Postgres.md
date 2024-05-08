### How to Install pgAdmin on Ubuntu 22.04
 [How to Install pgAdmin on Ubuntu 22.04](https://linuxgenie.net/how-to-install-pgadmin-on-ubuntu-22-04/)

  - Step 1: Install Curl
    ```
    sudo apt install curl
    ```
  - Step 2: Add Public Key Using Curl
      ```
      sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
      ```
  - Step 3: Add pgAdmin Repository
      ```
      sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'
      ```
  - Step 4: Update Server’s Packages
      ```
      sudo apt update
      ```
  - Step 5: Install pgAdmin
      ```
      sudo apt install pgadmin4 -y
      ```
  


### How To Install PostgreSQL on Ubuntu 22.04
  [How To Install PostgreSQL on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-postgresql-on-ubuntu-22-04-quickstart)
   - 1st To install PostgreSQL, first refresh your server’s local package index:
      ```
       sudo apt update
      ```
   - 2nd Then, install the Postgres package along with a -contrib package that adds some additional utilities and functionality:
       ```
       sudo apt install postgresql postgresql-contrib
       ```
   - 3rd run this command
      ```
      sudo -i -u postgres
      ```
   - 4th Then you can access the Postgres prompt by running:
      ```
      psql
      ```
  - 5th setup password for postgres User and Log in into the psql promt:
      ```
       sudo -u postgres psql
      ```
  - 6th Then in the psql console, change the password and quit
      ```
      postgres=# \password postgres
      Enter new password: <new-password>
      postgres=# \q
      ```
  - 7th run this command for showing pg_hba.conf file
      ```
      postgres=# SHOW hba_file;
      ```
  - 8th open a new terminal and paste this sudo nano /etc/postgresql/14/main/pg_hba.conf
      ```
      sudo nano /etc/postgresql/14/main/pg_hba.conf
      ```
  - 9th we find this type of value under a file
      ```
          default:
         local   all             postgres                             peer
      
         Change it: 
      
         local   all             postgres                             md5
      ```
  - 10th Then restarted the postgres service with the command
      ```
      sudo service postgresql restart
      ```
    
# How to enter Postgres using terminal
```
sudo su postgres
then psql
```

### How to check postgres is running
```
systemctl status postgresql
```

## How to restore sql file in postgres db
```
pg_restore -O -x -h localhost -U postgres -p 5434 -d trmisdb trmis_backend_backup_16_October_2023_11_00__AM.sql
```
## There is 1 other session using the database.database "exception_db" is being accessed by other users
### 1st step
```
SELECT pg_terminate_backend(pg_stat_activity.pid)
    FROM pg_stat_activity
    WHERE pg_stat_activity.datname = 'exception_db'(db_name);
```
### 2nd step
```
DROP DATABASE exception_db;
```
### Here is the command to pull the PostgreSQL Docker image:
 ```
  docker pull postgres
 ```
### You can set up a PostgreSQL Docker container with the name postgres_docker and expose it on port 5433. Here's an example command:
```
 docker run --name postgres_docker -e POSTGRES_PASSWORD=mysecretpassword -p 5433:5432 -d postgres:latest
```
### you can connect to PostgreSQL using the host localhost and port 5433:
```
 psql -h localhost -p 5433 -U postgres -d postgres
```
### Enter Docker postgres
```
 psql -U postgres
```
