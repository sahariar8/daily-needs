### How To Install and Use Docker on Ubuntu 22.04
[How To Install and Use Docker on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)

- Step 1 update your existing list of packages:
    ```
      sudo apt update
    ```
  
- Step 2 Next, install a few prerequisite packages which let apt use packages over HTTPS:
    ```
      sudo apt install apt-transport-https ca-certificates curl software-properties-common
    ```
  
- Step 3 Then add the GPG key for the official Docker repository to your system:
    ```
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gp
    ```
  
- Step 4 Add the Docker repository to APT sources:
    ```
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

- Step 5 Update your existing list of packages again for the addition to be recognized:

  ```
    sudo apt update
  ```
- Step 6 Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
  ```
    apt-cache policy docker-ce
  ```

- Step 7 Finally, install Docker:
  ```
   sudo apt install docker-ce
  ```
- Step 8 Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
  ```
   sudo systemctl status docker
  ```
- Step 9 To run docker commands without sudo
    ```
      sudo usermod -aG docker hachib-khan [your-current-username]

      sudo su hachib-khan [your-current-username]
    ```
  
### To copy an SQL file from your local PC to a Docker container, you can use the docker cp
```
docker cp quantlio.sql(file_name)  a3f371b6277c(container_id):/var/lib/mysql/
```

### Check if PostgreSQL is running: Verify if there is a PostgreSQL database running on your host machine that is already using port 5432. You can check this using the following command:
```
  sudo lsof -i :5432
```
### To enter a PostgreSQL container, you can use the docker exec command. Here's how you can do it:
```
docker exec -it eap_db_1 bash
or
docker exec -it a3f(container id) bash
```
### After running this command, you will be inside the PostgreSQL container, and you can run PostgreSQL commands as needed. If your container is running a PostgreSQL server, you can access the PostgreSQL command-line interface (CLI) by typing:
```
psql -U your_username -d your_database_name
```
