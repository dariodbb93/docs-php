---
title: music webserver on linux
subtitle: music webserver on linux
categories:
    - personal
---

In questa guida vedremo come realizzare un server linux dove possiamo ascoltare la musica. <br>

1. ci servirà un server VPS o comunque un server su cui installare ubuntu server
2. aggiornamento globale dei pacchetti a sistema 

```bash
sudo apt update
sudo apt upgrade
sudo apt install vim ffmpeg
```
3. creazione delle cartelle di sistema

```bash
sudo install -d -o <user> -g <group> /opt/navidrome
sudo install -d -o <user> -g <group> /var/lib/navidrome
```

4. ottenere la libreria navidrome
sostituisci la versione con quella desiderata, dai qui puoi vederle: https://github.com/navidrome/navidrome/releases

```bash
wget https://github.com/navidrome/navidrome/releases/download/v0.XX.X/navidrome_0.XX.X_linux_amd64.tar.gz -O Navidrome.tar.gz
sudo tar -xvzf Navidrome.tar.gz -C /opt/navidrome/
sudo chown -R <user>:<group> /opt/navidrome
```

5. crea un file di configurazione per navidrome

```bash
MusicFolder = "<library_path>"
```

6. crea il servizio per navidrome

```bash 
cd /etc/systemd/system/
sudo nano navidrome.service
```
7. incolla il template sostituendo utente e gruppo indicati in precedenzza

```bash
[Unit]
Description=Navidrome Music Server and Streamer compatible with Subsonic/Airsonic
After=remote-fs.target network.target
AssertPathExists=/var/lib/navidrome

[Install]
WantedBy=multi-user.target

[Service]
User=<user>
Group=<group>
Type=simple
ExecStart=/opt/navidrome/navidrome --configfile "/var/lib/navidrome/navidrome.toml"
WorkingDirectory=/var/lib/navidrome
TimeoutStopSec=20
KillMode=process
Restart=on-failure

# See https://www.freedesktop.org/software/systemd/man/systemd.exec.html
DevicePolicy=closed
NoNewPrivileges=yes
PrivateTmp=yes
PrivateUsers=yes
ProtectControlGroups=yes
ProtectKernelModules=yes
ProtectKernelTunables=yes
RestrictAddressFamilies=AF_UNIX AF_INET AF_INET6
RestrictNamespaces=yes
RestrictRealtime=yes
SystemCallFilter=~@clock @debug @module @mount @obsolete @reboot @setuid @swap
ReadWritePaths=/var/lib/navidrome

# You can uncomment the following line if you're not using the jukebox This
# will prevent navidrome from accessing any real (physical) devices
#PrivateDevices=yes

# You can change the following line to `strict` instead of `full` if you don't
# want navidrome to be able to write anything on your filesystem outside of
# /var/lib/navidrome.
ProtectSystem=full

# You can uncomment the following line if you don't have any media in /home/*.
# This will prevent navidrome from ever reading/writing anything there.
#ProtectHome=true

# You can customize some Navidrome config options by setting environment variables here. Ex:
#Environment=ND_BASEURL="/navidrome"
```
8. fai partire il servizio

```bash
sudo systemctl daemon-reload
sudo systemctl start navidrome.service
sudo systemctl status navidrome.service
```
9. ed infine

```bash
sudo systemctl enable navidrome.service
```

10. ottieni l'ip del tuo server linux

```bash
ip route
```

11. icollalo sul browser e carica la musica nella cartella specificata.