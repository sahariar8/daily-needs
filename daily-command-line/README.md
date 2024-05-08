### HOW TO INSTALL ERPNEXT VERSION 14 IN UBUNTU 22.04

### Installing NVM on Ubuntu
  - step 1
  ```
    sudo apt install curl
    curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
    source ~/.bashrc   
  ```
 - step 2 Install Node using nvm
   ```
     nvm install 18
   ```
### Install Redis Server
  ```
    sudo apt-get install redis-server
  ```
  - How to see Redis version
    ```
      redis-cli INFO server
    ```
    
### How to install bench
```
pip3 install frappe-bench
```
