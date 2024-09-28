Steps:
Create an EC2 Instance:


![image](https://github.com/user-attachments/assets/d929caad-c6b8-4558-83c7-6dab9c8c9e30)


Choose a cloud provider (AWS, Azure, GCP) and create an EC2 instance in the desired region.
Configure the instance with appropriate specifications (e.g., CPU, RAM, storage) based on your project requirements.
Open necessary security group rules to allow inbound traffic on port 80 (HTTP) and 443 (HTTPS) for web access and port 3306 (MySQL) for database connections.

Log in to the EC2 Instance: I used putty, you can use any terminal emulator of your choice.


Connect to your EC2 instance using SSH or a remote desktop connection.
Install Apache Server:

Update the package list:
Bash
sudo apt update

Install Apache:
Bash
sudo apt install apache2.

Verify Apache is running:
Access the instance's public IP address in a web browser. You should see a default Apache page.

Install MySQL Database:
Install MySQL server:
Bash
sudo apt install mysql-server

Secure the MySQL installation:
Bash
sudo mysql_secure_installation

Follow the prompts to set a root password and remove anonymous users, test accounts, and the database named test.
Install PHP:
Install PHP and its MySQL extension:
Bash
sudo apt install php libapache2-mod-php php-mysql

.

Verify PHP installation:
Bash
php -v

Creating a Virtual Host for Your Website
Create a virtual host configuration file for your project:

/etc/apache2/sites-available/projectlamp.conf

Apache
<VirtualHost *:80>
ServerName projectlamp
ServerAlias www.projectlamp
ServerAdmin webmaster@localhost
DocumentRoot /var/www/projectlamp
ErrorLog
/var/log/apache2/error.log
CustomLog /var/log/apache2/access.log combined
</VirtualHost>

Use code with caution.
Enable the virtual host:
Bash
sudo a2ensite projectlamp.conf

Restart Apache:
Bash
sudo systemctl restart apache2

Your project will now be accessible at your instance's URL http://external ip address. Replace the /var/www/projectlamp directory in the configuration file with the desired directory for your project files.

Step 5 — Enable PHP on the website
With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.

In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

sudo vim /etc/apache2/mods-enabled/dir.conf

<IfModule mod_dir.c>
#Change this:
#DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
#To this:
DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

After saving and closing the file, you will need to reload Apache so the changes take effect:

$ sudo systemctl reload apache2

Create a PHP script to test that PHP is correctly installed and configured on your server.

Create a new file named index.php inside your custom web root folder:$ vim /var/www/projectlamp/index.php

A blank file. Add the following text, which is valid PHP code, inside the file:

<?php
phpinfo();
Save and close the file, refresh the page and you will see a page similar to this:



Additional Notes
Configure your database (create databases, tables, users, etc.) using MySQL commands or tools like phpMyAdmin.
Develop your PHP applications and place them in the /var/www/projectlamp directory or a subdirectory.
Customize the virtual host configuration for additional features like SSL certificates, custom error pages, and more.
