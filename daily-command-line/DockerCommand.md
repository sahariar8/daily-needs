### Docker run if docker is off

```
sudo systemctl start docker
```
### Docker Status Check

```
sudo systemctl status docker
```

### Add current User in Docker Group

```
sudo usermod -aG docker $USER
```
### Run this command for Immediate user add in docker group

```
newgrp docker
```
### Restart cli after group add
```
sudo reboot
```

