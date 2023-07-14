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

## Addendum
If you choose the beta channel in plex media server settings, you will be informed of an update available within PMS, that normal "sudo apt update" and "sudo apt upgrade" commands will not be able to update/upgrade. You will be required to go to https://www.plex.tv/media-server-downloads/, choose Linux, plex pass if you have it, and then Ubuntu/Debian 8+ 64bit.

![plex2](https://github.com/epicinsomniac/dock/assets/135930881/5bc56a94-fa61-4716-ab69-f414aad94115)

![plex3](https://github.com/epicinsomniac/dock/assets/135930881/f15ede7e-dec1-4bec-a322-3724f5da5133)
then simply:

```wget https://downloads.plex.tv/plex-media-server-new/1.32.5.7318-0b5fb6462/debian/plexmediaserver_1.32.5.7318-0b5fb6462_amd64.deb```


```sudo dpkg -i plexmediaserver_1.32.5.7318-0b5fb6462_amd64.deb```
