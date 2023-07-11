# dock
My Debian 11-12, VPS, Cloudflare DNS, Docker stack foundation and framework:

# SSH into Debian 11-12 VPS

```apt update && apt -y upgrade && apt -y install wget curl git nano sudo exa tree build-essential```

# Restart

```shutdown -r now```

# SSH into VPS

```adduser USERNAME```

# Add USERNAME to sudo

```usermod -aG sudo USERNAME```

# login as new user

```su USERNAME```

# Setup key

```mkdir ~/.ssh && touch ~/.ssh/authorized_keys``` <br>
```chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys``` <br>
```nano ~/.ssh/authorized_keys``` <br>
 |_ paste in key <br>
```sudo nano /etc/ssh/sshd_config``` <br>
 |_ edit the following <br>
 | <br>
 |_ Port YOUR-CHOSEN-PORT-NUMBER "example: Port 333" <br>
 |_ PermitRootLogin no <br>
 |_ PubkeyAuthentication no <br>
 |_ PasswordAuthentication no <br>
 | <br>
 |_ add to the bottom of the file <br>
 | <br>
 |_ Match User USERNAME <br>
 |_ PubkeyAuthentication yes <br>
 
# Restart and check status of SSHD service

```sudo service sshd restart && sudo service sshd status```<br>
 |_ Hit "q" to exit.

# Setup putty

Add new client, use VPS IP and chosen port. <br>
Left menu > Connection > Data > Auto-login username: USERNAME <br>
Left menu > SSH > Auth: Browse to private key .ppk <br>
Left menu > Session > Saved Sessions box: Give connection a name > Save <br>

# Setup putty agent

Add private key .ppk file > enter passphrase when prompted.

# Test SSH

Open second SSH connection to server. <br>
Expected behavior is to connect without any user interaction.

# Git source and samples

```cd ~/```<br>
```git clone https://github.com/epicinsomniac/dock.git dock/```<br>
```cd dock```<br>
```cp .env-sample .env```<br>
```cp docker-compose.sample.yml docker-compose.yml```<br>

# Setup bashrc and aliases

```cp .bashrc-sample ~/.bashrc```<br>
```cd ~/```<br>
```touch .bash_profile```<br>
```nano .bash_profile```<br>
 |_ Paste the following:<br>

``` [ -f "$HOME/.bashrc" ] && source "$HOME/.bashrc" ```<br>

# Install Docker and plugins

```sudo apt-get update ```<br>
```sudo apt-get -y install ca-certificates curl gnupg ```<br>

```sudo install -m 0755 -d /etc/apt/keyrings ```<br>
```curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg ```<br>
```sudo chmod a+r /etc/apt/keyrings/docker.gpg ```<br>

```echo \```<br>
```  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \``` <br>
```  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \``` <br>
```  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null``` <br>
  
```sudo apt update```

```sudo apt -y install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin```

# Test Docker and Docker Compose

```sudo docker version```

```sudo docker compose version```


# Addendum for pci passthrough NVIDIA on proxmox > debian vm

Download NVIDIA Driver<br>
Before we install the NVIDIA driver, we need to install the linux header files and dkms so when the linux kernel is updated the NVIDIA driver will automatically recompile<br>

```sudo apt-get install dkms linux-headers-$(uname -r)```<br>
Now we need to install the GPU Driver, and this is where things diverge from the instructions on 3os.org.

Go to https://www.nvidia.com/Download/index.aspx?lang=en-us and search for the driver you need:

According to the NVIDIA developer zone: Create a file:

```sudo nano /etc/modprobe.d/blacklist-nouveau.conf```

With the following contents:

```blacklist nouveau```<br>
```options nouveau modeset=0```<br>

Regenerate the kernel initramfs:

```sudo update-initramfs -u```<br>

Finally, reboot:

```sudo reboot```<br>
