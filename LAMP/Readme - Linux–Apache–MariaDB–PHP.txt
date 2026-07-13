Server Setup Steps
 Firewall
 Install Firewall

MariaDB
 Install MariaDB

 Configure MariaDB

 Start MariaDB

 Configure Firewall

 Configure Database

 Load Data

Apache & PHP
 Install httpd

 Install PHP

 Configure Firewall

 Configure httpd

 Start httpd

 Download Code

 Test



Install Firewall

sudo yum install firewalld
sudo service firewalld start
sudo systemctl enable firewalld

Install MariaDB

sudo yum install mariadb-server

Configure MariaDB

sudo vi /etc/my.cnf  # configure the file with the right port

Start MariaDB

sudo service mariadb start
sudo systemctl enable mariadb

Configure Firewall

sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp
sudo firewall-cmd --reload

Configure Database

mysql
MariaDB > CREATE DATABASE ecomdb;
MariaDB > CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
MariaDB > GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
MariaDB > FLUSH PRIVILEGES;

Load Data

mysql < db-load-script.sql

Install httpd & PHP

sudo yum install -y httpd php php-mysql

Configure Firewall

sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
sudo firewall-cmd --reload

Configure httpd

sudo vi /etc/httpd/conf/httpd.conf
# configure DirectoryIndex to use index.php instead of index.html

Start httpd

sudo service httpd start
sudo systemctl enable httpd

Download Code

sudo yum install -y git
git clone https://github.com/<application>.git /var/www/html/
# Update index.php to use the right database address, name and credentials

Test

curl http://localhost