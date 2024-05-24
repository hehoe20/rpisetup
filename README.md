# RPI setup
```bash
# write Ubuntu image to HD/SD, LAN connected to router, boot:
# login via ssh (use putty or similar), ubuntu:ubuntu
# change pass and login again with new pass for ubuntu user
#
sudo apt update
sudo apt upgrade
sudo apt install ca-certificates curl gnupg lsb-release linux-modules-extra-raspi
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

# logout and login

# WEBMIN:
curl -fsSL https://download.webmin.com/jcameron-key.asc | sudo gpg --dearmor -o /usr/share/keyrings/webmin.gpg
sudo echo "deb [signed-by=/usr/share/keyrings/webmin.gpg] http://download.webmin.com/download/repository sarge contrib" >> /etc/apt/sources.list
sudo apt update
sudo apt install webmin

# PORTAINER AGENT (if more than one docker host):
docker run -d -p 9001:9001 --name portainer_agent --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/volumes:/var/lib/docker/volumes portainer/agent:latest
```
