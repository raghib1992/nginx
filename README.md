### Process to generate SSL certificatesudo apt install letsencrypt
# UBUNTU

## Step 1 – Installing the «Let’s Encrypt» package
sudo apt install letsencrypt
sudo systemctl status certbot.timer

## Step 2 – Standalone server for getting the «Let’s Encrypt» SSL certificate

sudo certbot certonly --standalone --agree-tos --preferred-challenges http -d domain-name.com

## Step 3 – Automatic installation of the SSL certificate on nginx and Apache web servers
apt install python3-certbot-nginx
apt install python3-certbot-apache

# Run this command for nginx: or  this for Apache:
sudo certbot --nginx --agree-tos --preferred-challenges http -d domain-name.com
sudo certbot --apache --agree-tos --preferred-challenges http -d domain-name.com

## Step 4 – «Let’s Encrypt» Wildcard SSL certificate
sudo certbot certonly --manual --agree-tos --preferred-challenges dns -d domain-name.com -d *.domain-name.com
