# Deployment Instructions for the Organizações Garyana Website

## 1. Prerequisites
- A VPS running Ubuntu 20.04 or similar.
- SSH access to the server.
- Domain name pointed to your VPS IP address.
- sudo privileges on the VPS.

## 2. Step-by-Step Setup Guide
### Step 1: Connect to Your VPS
Use SSH to connect to your VPS:
```bash
ssh user@your_vps_ip
```
### Step 2: Update Package List
```bash
sudo apt update && sudo apt upgrade -y
```
### Step 3: Install Required Packages
Install Nginx, Git, and PHP:
```bash
sudo apt install nginx git php-fpm php-mysql -y
```
### Step 4: Clone the Repository
Clone the Organizações Garyana repository:
```bash
git clone https://github.com/your_username/site.ORG-GARYANA.git
```
### Step 5: Configure Nginx
Create a new Nginx configuration file:
```bash
sudo nano /etc/nginx/sites-available/garyana
```
Add the following content:
```
server {
    listen 80;
    server_name your_domain.com;

    root /path/to/site.ORG-GARYANA;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```
### Step 6: Enable the Configuration
Link the configuration file:
```bash
sudo ln -s /etc/nginx/sites-available/garyana /etc/nginx/sites-enabled/
```
### Step 7: Test Nginx Configuration
```bash
sudo nginx -t
```
### Step 8: Restart Nginx
```bash
sudo systemctl restart nginx
```

## 3. SSL Certificate Installation
### Step 1: Install Certbot
```bash
sudo apt install certbot python3-certbot-nginx -y
```
### Step 2: Obtain an SSL Certificate
Run the following command:
```bash
sudo certbot --nginx -d your_domain.com
```
### Step 3: Verify SSL Certificate Auto-Renewal
```bash
sudo certbot renew --dry-run
```

## 4. Troubleshooting Tips
- **Nginx not starting:** Check for syntax errors using `sudo nginx -t`.
- **Website not reachable:** Ensure DNS records are correctly pointed.
- **Permission denied errors:** Check file permissions in your web root.

## Conclusion
Following these instructions will help you set up the Organizações Garyana website on your VPS successfully. If you encounter any issues, refer to the troubleshooting tips or seek further help.
