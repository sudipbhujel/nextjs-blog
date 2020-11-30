---
title: 'Essential Knowledge for Fullstack Engineer'
date: '2020-11-30'
---

## Command line

- cd - change directory
- ls - list directory contents
- pwd - print working directory
- mkdir - make directory
- rmdir - remove directory

- cat - show file contents
- man - command manual
- less - show file contents by page
- rm - remove file
- echo - repeat input

```bash
echo $0
```

## TCP and UDP

TCP is lossless and has error connection, error checking. UDP is one way of communication that is one way blast of information. TCP needs back and froth SYN and ACK for the connection.

```bash
ping twitter.com
```

```bash
man traceroute
traceroute google.com
```

## VIM

## Commands

insert mode `i`

command mode `ESC`

last line mode `:`

### How to quit VIM?

`ESC :q!`

## Make user in UBUNTU

```bash
ssh-keygen # for new public and private key
```

```
# Create a new user
sudo adduser $USERNAME

# Add user to "sudo" group
sudo usermod -aG $USERNAME # Give sudo permission to new user
sudo usermod -aG sudo $USERNAME

# Check sudo access
sudo cat /var/log/auth.log
```

### Server Setup

```bash
# Change to home directory
cd ~

# Create a new directory if it doensn't exist
mkdir -p ~/.ssh

# Create authorized_keys file and paste PUBLIC key
vi ~/.ssh/authorized_keys

# Exit
exit

# Login with new user
ssh $USERNAME@IP_ADDRESS

# Change file permissions
chmod 644 ~/.ssh/authorized_keys

# Disable root login
sudo vi etc/ssh/sshd_config # Find permitRootLogin and set is `no`

# Restart the ssh daemon
sudo service sshd restart

# Disable root login
sudo vi /etc/ssh/sshd_config
```

## Nginx

- Reverse proxy
- Web server
- Proxy server

```sh
# Install nginx
sudo apt install nginx

# Start nginx
sudo service nginx start

# Show nginx configuration
sudo less /etc/nginx/sites-available/default

root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
```

### Configuration

```bash
sudo vi /var/www/html/index.html

# Insert content
hello, everyone!
```

## NodeJS

```bash
# Install NodeJS and npm
sudo apt install nodejs npm

# Install git
sudo apt install git

# Change ownership of the www directory to the current user
sudo chown -R $USER:$USER /var/www

# Create application directory
mkdir /var/www/app

# Move into app directory and initialize empty git repo
cd /var/www/app && git init

# Create directories
mkdir -p ui/js ui/html ui/css

# Create empty app file
touch app.js

# Initialize project

npm init

# Install i express --save

# edit app

vi app.js

```

### Edit app.js

```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello, world!')
})

app.listen(port, () => {
    console.log(`Example app listening on port ${port}!`))
    }
```

domain --> IP --> NGINX --> Express

## Proxy pass (NGINX)

```bash
location / {
    proxy_pass URL_TO_PROXY_TO;
}

# Edit nginx config
sudo vi /etc/nginx/sites-available/default
```

## Process Manager

`Background process runner`

```bash
# Instal PM2
sudo npm i -g pm2 # Alternative is forever

# Start PM2
pm2 start app.js

# Setup auto restart
pm2 startup
```

## Git Repository

1. Create git repository
2. Create SSH key
3. Add SSH key to Github
4. Add remote repo
5. Push local repository to Github

## Standard Streams

- Standard output
  - `stdout`
- Standard input
  - `stdin`
- Standard error
  - `stderr`

## Finding things

`find /bar -name foo.txt`

Useful options

- -name
- -type
- -empty
- -executable
- -writable

```bash
# Find all log files
sudo find /var/log/nginx/ -type f -name "*.log"

# Find all directories with the name log
find / -type d -name log

grep -i 'sudip' /var/www

zgrep FILE # search inside gzip file

# Find running node processes
ps aux | grep node
# a = show processes for all users
# u = display the process's user/owner
# x = also show processes not attached to a terminal
```

## Nginx-subdomain

```bash
server {
    listen 80;
    listen [::]80; # IPV6 notation

    server_name test.thrivenexus.ml;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

## Security

Application Updates

```bash
# Install unattended upgrades
sudo apt install unattended-upgrades

# View conf file
cat /etc/apt/apt.conf.d/50unattended-upgrades
```

## Firewall

`A network security device that motitors incoming and outgoing network traffic and decides whether to allow or block specific traffic based on a defined set of security rules.`

`nmap` is port scanner.

```bash
sudo apt install nmap

# Run nmap
nmap YOUR_SERVER_IP_ADDRESS

# Run nmap with more service/version info
nmap -sV YOUR_SERVER_IP_ADDRESS

# Check firewall status
sudo ufw status

# Enable ssh
sudo ufw allow ssh

# Enable firewall
sudo ufw enable
```

## Update nodejs

```bash
# Download setup script from nodesource
curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh

# Run script
sudo bash nodesource_setup.sh

# Install nodejs
sudo apt install nodejs
```

## Status Codes

1xx Information
2xx Success
3xx Redirect
4xx Client error
5xx Server error

## Encryption

ENCRYPT the site with [certbot](https://certbot.eff.org/)

## Add HTTP2

```bash
sudo vi /etc/nginx/sites-available/default

listen [::]:443 http2 ssl ipv6only=on; # managed by Certbot
listen 443 http2 ssl; # managed by Certbot
```
