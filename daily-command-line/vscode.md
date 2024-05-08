### How to Install Visual Studio Code on Ubuntu 22.04
[How to Install Visual Studio Code on Ubuntu 22.04](https://linuxhint.com/install-visual-studio-code-ubuntu22-04/)
  - Step 1: Update the system
    ```
    sudo apt update && sudo apt upgrade -y
    ```
  - Step 2: Install packages
      ```
      sudo apt install software-properties-common apt-transport-https wget -y
      ```
  - Step 2: Import repository
      ```
      wget -O- https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor | sudo tee /usr/share/keyrings/vscode.gpg
      ```
      ```
      echo deb [arch=amd64 signed-by=/usr/share/keyrings/vscode.gpg] https://packages.microsoft.com/repos/vscode stable main | sudo tee /etc/apt/sources.list.d/vscode.list
      ```
  - Step 4: Update the system again
      ```
      sudo apt update
      ```
  - Step 5: Install the editor
     ```
     sudo apt install code
     ```

### How to back alignment in vs code
```
shift tab
```

