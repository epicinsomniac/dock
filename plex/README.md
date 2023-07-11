# Plex Media Server

### Update
```sudo apt update && sudo apt upgrade -y```
### Install packages
```sudo apt install apt-transport-https curl vim wget sudo gnupg2 -y```

### Add the Plex repository using the below command & Import the GPG keys for the repository.
```echo "deb https://downloads.plex.tv/repo/deb public main" | sudo tee /etc/apt/sources.list.d/plexmediaserver.list```

```curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -```

### Update the APT package index.
```sudo apt update```<br>
### Install
```sudo apt install plexmediaserver```
### Dependency Tree:
![plex1](https://github.com/epicinsomniac/dock/assets/135930881/6766e032-f177-49a1-89d9-77383669f294)

### Start Plex Media Server
```sudo systemctl start plexmediaserver```

### !!!! Enable Plex Media Server !!!!
```sudo systemctl enable plexmediaserver```
