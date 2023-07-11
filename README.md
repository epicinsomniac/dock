# dock
My Debian 11-12, VPS, Cloudflare DNS, Docker stack foundation and framework:

# Requisites or helpful tools:
## Windows
## notepad++ <br>
[notepad++](https://notepad-plus-plus.org/downloads/)
![notepage++logo](https://github.com/epicinsomniac/dock/assets/135930881/2b858bff-a660-4485-8ad2-3745d82f69a7)<br>
## filezilla <br?
[filezilla](https://filezilla-project.org/)
![filezilla1](https://github.com/epicinsomniac/dock/assets/135930881/e773afb8-d298-4801-aa10-4ba8b9e8c87b)
![filezilla2](https://github.com/epicinsomniac/dock/assets/135930881/adcd345a-b633-46e3-b370-0ae5f3e0e8f1)

## Debian


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
```source . ~/.bashrc```

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

```sudo docker version```<br>
or use the alias that was set in .bashrc<br>
```sdv```<br>
![sdv](https://github.com/epicinsomniac/dock/assets/135930881/3b9cf337-308a-4300-b8c3-a4fa8b27273a)

```sudo docker compose version```<br>
or use the aliase that was set in .bashrc<br>
```sdcv```
![sdcv](https://github.com/epicinsomniac/dock/assets/135930881/a2b81c4b-a98f-4424-a627-eb206f9d5e70)



# Addendum for pci passthrough NVIDIA on proxmox > debian vm

Download NVIDIA Driver<br>
Before we install the NVIDIA driver, we need to install the linux header files and dkms so when the linux kernel is updated the NVIDIA driver will automatically recompile<br>

```sudo apt-get install dkms linux-headers-$(uname -r)```<br>
Now we need to install the GPU Driver, and this is where things diverge from the instructions on 3os.org.

Go to https://www.nvidia.com/Download/index.aspx?lang=en-us and search for the driver you need:<br>
![nvidia-driver](https://github.com/epicinsomniac/dock/assets/135930881/9b32f8f9-ea27-405a-8151-fff020c431aa)<br>
![nvidia-driver2](https://github.com/epicinsomniac/dock/assets/135930881/5b2e5e0d-a41f-48ee-94cc-7b84f1d1e08f)<br>
![nvidia-driver3](https://github.com/epicinsomniac/dock/assets/135930881/64d66d1e-7e5e-4538-abd1-a46fd470b75e)<br>
![nvidia-driver4](https://github.com/epicinsomniac/dock/assets/135930881/4df1e8ca-1678-48ba-b6d3-092e02b4f531)<br>




According to the NVIDIA developer zone: Create a file:

```sudo nano /etc/modprobe.d/blacklist-nouveau.conf```

With the following contents:

```blacklist nouveau```<br>
```options nouveau modeset=0```<br>

Regenerate the kernel initramfs:

```sudo update-initramfs -u```<br>

Finally, reboot:

```sudo reboot```<br>

Verify Driver Installation<br>
You should be able to verify that the system recognizes the GPU by running nvidia-smi

```nvidia-smi```<br>
![nvidia-smi](https://github.com/epicinsomniac/dock/assets/135930881/acc5f4e9-7fd6-4316-99bd-0a4d1016d3e8)
