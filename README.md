STEPS IN CREATING A LAMP STACK PROJECT.
Create an EC2 Instance in a cloud environment (AWS, AZURE, GCP)
Log in to your EC2 instance and install the Apache server.
Install mysqldatabase
Install PHP.
 

Installing Apache on the ec2 instance.
#update a list of packages in the package manager
$ sudo apt update
#run apache2 package installation
$ sudo apt install apache2
Log in to your ec2instance public IP to confirm Apache is running.
Installing mysl on the ec2 instance.
$ sudo apt install MySQL-server
When the installation is finished, log in to the MySQL console by typing:
$ sudo MySQL
$ exit
Installing PHP and other dependencies.
$ sudo apt install php libapache2-mod-php php-mysql
php -v (to confirm the installation)

 Creating a Virtual Host for your Website using Apache
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
