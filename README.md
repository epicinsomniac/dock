# dock
My Debian 11, VPS, Cloudflare DNS, Docker stack foundation and framework:

# SSH into Debian 11 VPS

apt update && apt -y upgrade && apt -y install wget curl git nano sudo exa tree build-essential

# Restart

shutdown -r now

# SSH into VPS

adduser USERNAME

# Add USERNAME to sudo

usermod -aG sudo USERNAME

# login as new user

su USERNAME

# Setup key

mkdir ~/.ssh && touch ~/.ssh/authorized_keys
chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
nano ~/.ssh/authorized_keys
 |_ paste in key
sudo nano /etc/ssh/sshd_config
 |_ edit the following
 |
 |_ Port YOUR-CHOSEN-PORT-NUMBER example: Port 333
 |_ PermitRootLogin no
 |_ PubkeyAuthentication no
 |_ PasswordAuthentication no
 |
 |_ add to the bottom of the file
 |
 |_ Match User USERNAME
 |_ PubkeyAuthentication yes
 
# Restart and check status of SSHD service

sudo service sshd restart && sudo service sshd status

# Setup putty

Add new client, use VPS IP and chosen port.
Left menu > Connection > Data > Auto-login username: USERNAME
Left menu > SSH > Auth: Browse to private key .ppk 
Left menu > Session > Saved Sessions box: Give connection a name > Save

# Setup putty agent

Add private key .ppk file > enter passphrase when prompted.

# Test SSH

Open second SSH connection to server. Expected behavior is to connect without any user interaction.

# Install Docker and plugins

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
sudo apt update

sudo apt -y install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker and Docker Compose

sudo docker version

sudo docker compose version


