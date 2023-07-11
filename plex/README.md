# Plex Media Server

# Update
```sudo apt update && sudo apt upgrade -y```<br>
# Install packages
```sudo apt install apt-transport-https curl vim wget sudo gnupg2 -y```<br>

# Add the Plex repository using the below command & Import the GPG keys for the repository.
```echo "deb https://downloads.plex.tv/repo/deb public main" | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
```<br>
```curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
```<br>

# Update the APT package index.
```sudo apt update```<br>
# Install
```sudo apt install plexmediaserver```<br>

Dependency Tree: