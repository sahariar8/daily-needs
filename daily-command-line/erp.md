### HOW TO INSTALL ERPNEXT VERSION 14 IN UBUNTU 22.04

### A STEP BY STEP GUIDE
- In this article, I will take a step-by-step approach to configure our newly installed ubuntu 22.04 OS to set up an environment and install ERPNext version 14. Let’s get to work!

### Prerequisites
- The below prerequisites are advised in order to get an optimal functionality of ERPNext on your server.

### Software Requirements
- Updated Ubuntu 22.04
- A user with sudo privileges
- Python 3.10+
- Node.js 18
- Redis Server

### Database
- MariaDB Server 10.8

### Hardware Requirements
- 4GB RAM
- 40GB Hard Disk

Server Settings Update and Upgrade Packages sudo apt-get update -y sudo apt-get upgrade -y Create a new user – (bench user)

In linux, the root user processes escalated privileges to perform any tasks within the system. This is why it is not advisable to use this user on a daily basis. We will create a user that we can use, and this will be the user we will also use as the Frappe Bench User.

  ```
    sudo apt update
    sudo adduser [frappe-user]
    sudo usermod -aG sudo [frappe-user]
    sudo su [frappe-user] 
    cd /home/[frappe-user]
    Ensure you have replaced [frappe-user] with your username. eg. sudo adduser frappe
  ```

### Install Required Packages
A software like ERPNext, which is built on Frappe Framework, requires a number of packages in order to run smoothly. These are the packages we will be installing in this step.

### Install GIT

  ```
    sudo apt-get install git
  ```

### Install Python
- ERPNext version 14 requires Python version 3.10+. This is what we will install in this step.
  
    ```
      sudo apt-get install python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils
    ```
  
### Install Python Virtual Environment

- A virtual environment helps in managing the dependencies for one software at one place, without having to interfere with other sections in the computer or server in which the software is running.
  
    ```
      sudo apt-get install python3.10-venv
    ```
  
### In case of Ubuntu 23 and Python 3.11.6 follow

  ```
    sudo apt-get install python3-dev python3.11-dev python3-setuptools python3-pip python3-distutils software-properties-common xvfb libfontconfig wkhtmltopdf libmysqlclient-dev -y
    
    sudo apt-get install python3.11-venv -y
  ```

### Install Software Properties Common

- Software Properties Common will help in repository management.
    
    ```
      sudo apt-get install software-properties-common
    ```
  
### Install MariaDB

ERPNext is built to naively run on MariaDB. The team is working to have the same working on PostgreSQL, but this is not ready yet.

  ```
    sudo apt install mariadb-server mariadb-client
  ```

### Or Install MariaDB on Docker

  ```
    docker run -d --restart always -p 3306:3306 --name mariadb-10.8 --env MARIADB_ROOT_PASSWORD=nazmul -v /home/nazmul/Desktop/DevOps/inneed-projects/erpnext/conf/:/etc/mysql/conf.d mariadb:10.8
  ```

### If You don't have Docker installed in your machine then install docker

  ```
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    
    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    
    docker -v
    
    docker compose version
  ```

### To run docker commands without sudo
  ```
    sudo usermod -aG docker [your-current-username]
    
    sudo su [your-current-username]
  ```

### Install Redis Server

  ```
    sudo apt-get install redis-server
  ```

### Install other packages

- ERPNext functionality also relies on other packages we will install in this step. These will load fonts, PDFs, and other resources to our instance.
  ```
    sudo apt-get install xvfb libfontconfig wkhtmltopdf
    sudo apt-get install libmysqlclient-dev
  ```
  
### Configure MYSQL Server

If you use mariadb/mysql db with docker then skip this step

- Setup the server
  ```
    sudo mysql_secure_installation
  ```
- When you run this command, the server will show the following prompts. Please follow the steps as shown below to complete the setup correctly.
    ```
      "Enter current password for root: (Enter your SSH root user password) Switch to unix_socket authentication [Y/n]: Y Change the root password? [Y/n]: Y It will ask you to set new MySQL root password at this step. This can be different from the SSH root user password. Remove anonymous users? [Y/n] Y Disallow root login remotely? [Y/n]: N This is set as N because we might want to access the database from a remote server for using business analytics software like Metabase / PowerBI / Tableau, etc. Remove test database and access to it? [Y/n]: Y Reload privilege tables now? [Y/n]: Y
    ```
  
### Edit MYSQL default config file

  ```
    apt update
    apt install nano
    nano /etc/mysql/my.cnf
  ```

- Add the following block of code exactly as is:
    
  ```
    [mysqld]
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci
    
    [mysql]
    default-character-set = utf8mb4
  ```

- Restart the MYSQL Server
  
  ```
    sudo service mysql restart
  ```

### Instal CURL, Node, NPM and Yarn
### Install CURL
  ```
    sudo apt install curl
  ```

### Install Node
  ```
    curl -o- https://raw.githubusercontent.com/creationix/nvm/master/install.sh > install_nvm.sh
    bash install_nvm.sh
  ```
  
  ```
    source ~/.profile
  ```
- example
  
  ```
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
  ```

- Install node 18.
  
  ```
    nvm install 18
  ```

### Install NPM

  ```
    sudo apt-get install npm
  ```

### Install Yarn

  ```
    sudo npm install -g yarn
  ```

### Install Frappe Bench
  
  ```
    sudo pip3 install frappe-bench
  ```

### Initialize Frappe Bench

  ```
    bench init --frappe-branch version-14 [your-erp-project-name]
    
    cd [your-erp-project-name]
  ```

### Change user directory permissions
This will give the bench user execution permission to the home directory.

  ```
    chmod -R o+rx /home/[frappe-user]
  ```

### Create a New Site

A site is a requirement in ERPNext, Frappe and all the other apps we will be needing to install. We will create the site in this step.

  ```
    bench new-site [site-name] --db-name [your-preferred-db-name] its for local mysql server
    bench use [site-name]  or
    echo "[your-site-name]" > sites/currentsite.txt

    or If we use docker db we need to define port
    bench new-site inneed_erp_site --db-name inneed_erp_db --db-port 3307
  ```

### Install ERPNext and other Apps

Download all the apps we want to install The first app we will download is the payments app. This app is required when setting up ERPNext.

  ```
    bench get-app payments
    bench get-app --branch version-14 erpnext
    bench get-app --branch rafatul https://git.inneedcloud.com.bd/nazmul/inneed-erp.git
    bench get-app hrms
  ```

### Install all the apps on our site

  ```
    bench --site [site-name] install-app erpnext
    bench --site [site-name] install-app hrms
  ```

Install all the other apps you downloaded in the same way. For example, if you downloaded the human resource app, use the below command to install it.


### We have successfully setup ERPNext version 14 on ubuntu 22.04. You can start the server by running the below command:

  ```
    bench start
  ```

  ```
    "If you didn’t have any other ERPNext instance running on the same server, ERPNext will get started on port 8000. If you visit [YOUR SERVER IP:8000], you should be able to see ERPNext version 14 running.
  ```

  ```
    "Please note that instances which are running on develop mode, like the one we just setup, will not get started when you restart your server. You will need to run the bench start command every time the server restarts.
  ```
In the below steps, we will learn how to deploy the production mode.

### Setting ERPNext for Production

### Enable Scheduler
  ```
    bench --site [site-name] enable-scheduler
  ```

### Disable maintenance mode

  ```
    bench --site [site-name] set-maintenance-mode off
  ```

### Setup production config

  ```
    sudo bench setup production [frappe-user]
  ```

### Setup NGINX to apply the changes

  ```
    bench setup nginx
  ```

### Restart Supervisor and Launch Production Mode
  ```
    sudo supervisorctl restart all
    sudo bench setup production [frappe-user]
  ```
- If you are prompted to save the new/existing config file, respond with a Y.
  
  ```
    "When this completes doing the settings, your instance is now on production mode and can be accessed using your IP, without needing to use the port.
    
    This also will mean that your instance will start automatically even in after restart the server.
  
  ```
### Restore ERPNext from backup files
  ```
    bench --site site.name --force restore [database_file] --with-private-files [private_file] --with-public-files [public_file]
  
  ```
```
  "All the best! 🙂

```
