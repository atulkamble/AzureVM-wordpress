# 🚀 WordPress Setup on Ubuntu (Apache + MariaDB + PHP)

## 📌 Overview

This guide helps you install and configure **WordPress** on an Ubuntu server using:

* Apache Web Server
* MariaDB Database
* PHP

---

## 🔐 Step 1: Connect to Server

```bash
cd Downloads
chmod 400 wordpress.pem
ssh -i wordpress.pem azureuser@20.9.148.79
```

---

## 📦 Step 2: Update System

```bash
sudo apt update -y
sudo apt list --upgradable
sudo apt upgrade -y
```

---

## 🧰 Step 3: Install Required Packages

```bash
sudo apt install -y apache2 php php-mysql mariadb-server wget unzip
```

### ✅ Verify Installation

```bash
php --version
apache2 --version
mariadb --version
unzip --version
wget --version
```

---

## ⚙️ Step 4: Start & Enable Services

```bash
sudo systemctl start apache2
sudo systemctl enable apache2

sudo systemctl start mariadb
sudo systemctl enable mariadb
```

---

## 🗄️ Step 5: Configure Database

```bash
sudo mysql -u root -p
```

### Run inside MySQL:

```sql
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'StrongPassword123';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

---

## 🌐 Step 6: Download and Configure WordPress

```bash
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo rsync -av wordpress/* /var/www/html/
```

## 📁 Step 7: Set Permissions

```bash
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
```

---

## ⚙️ Step 8: Configure WordPress

```bash
cd /var/www/html
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

### Update DB Config:

```php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'StrongPassword123');
define('DB_HOST', 'localhost');
```

---

## 🔄 Step 9: Restart Apache

```bash
sudo systemctl restart apache2
```

---

## 🧹 Step 10: Remove Default Page

```bash
sudo rm /var/www/html/index.html
```

---

## 🌐 Step 11: Access WordPress

Open in browser:

```
http://20.9.148.79/wp-admin
```
```
http://20.9.148.79/wp-login.php
```
set username and password 
```
admin
Admin@123
```

---

## ✅ Final Result

* WordPress Login Page Accessible
* Apache Running
* Database Connected

---

## ⚠️ Important Notes (Production)

* Use strong passwords 🔐
* Enable firewall (`ufw allow 80,443`)
* Setup SSL (Let’s Encrypt)
* Take regular backups

---
