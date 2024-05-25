# RPI setup
## Docker CE
write Ubuntu image to HD/SD, LAN connected to router, boot:  
login via ssh (use putty or similar), ubuntu:ubuntu  
change pass and login again with new pass for ubuntu user  
```bash
sudo apt update
sudo apt upgrade
sudo apt linux-modules-extra-raspi
sudo apt install ca-certificates curl gnupg lsb-release 
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin docker-compose
sudo apt install net-tools usbutils aptitude
sudo apt install python3-pip python-is-python3 p7zip-full
sudo aptitude full-upgrade
sudo groupadd docker
sudo usermod -aG docker ${USER}
```
logout and login  
## Webmin
```bash
curl -fsSL https://download.webmin.com/jcameron-key.asc | sudo gpg --dearmor -o /usr/share/keyrings/webmin.gpg
sudo echo "deb [signed-by=/usr/share/keyrings/webmin.gpg] http://download.webmin.com/download/repository sarge contrib" >> /etc/apt/sources.list
sudo apt update
sudo apt install webmin
```
## Portainer Enterprise Edition
```bash
docker stop portainer
docker rm portainer
sudo docker pull portainer/portainer-ee:latest
docker run -d -p 8000:8000 -p 9000:9000 -p 9443:9443 \
    --name=portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /home/ubuntu/portainer/data:/data \
    portainer/portainer-ee:latest
```
## Portainer Agent (if more than one docker host):
```bash
docker run -d -p 9001:9001 --name portainer_agent --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/volumes:/var/lib/docker/volumes portainer/agent:latest
```
### Usefull links
[bash history](https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps)
