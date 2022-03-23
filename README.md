# lamp-server-install-ubuntu
lamp server install ubuntu
# About LAMP
The shortened form stands for Linux, Apache, MySQL, and PHP that is used to set up web servers. The words most often used to describe LAMP are stable, simple, and powerful. It is considered as a stack is on the ground that each level infers off it's base layer. In the Working framework, Linux, is the base layer. At that point Apache, the web server sits on the operating system, and then database stores all the data served by the web server, and PHP or any other P* scripting language is utilized to drive and show all the information, and consider client connection.
# Create file for script
```sh
sudo nano lamp.sh
```
then pest code and save
```sh
#!/bin/bash
sudo apt-get update
sudo apt-get -y install apache2
sudo apt install php7.3 php7.3-common php7.3-mysql php7.3-xml php7.3-xmlrpc php7.3-curl php7.3-gd php7.3-imagick php7.3-cli php7.3-dev php7.3-imap php7.3-mbstring php7.3-opcache php7.3-soap php7.3-zip php7.3-intl -y
sudo service apache2 restart
sudo apt-get -y install mysql-server
sudo mysql_secure_installation
sudo systemctl restart apache2 
```
Answer Y for yes, or anything else to continue without enabling.

```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
```
If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.

```
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```
Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user dispenses the use of a password, even when one is set, you should define a strong password here as an additional safety measure. We’ll talk about this in a moment.

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter Y for “yes” at the prompt:

```
Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
```
type your password ex.{mysql@123}

When you’re finished, test if you’re able to log in to the MySQL console by typing:

```sh
sudo mysql -u root -p
```
This will connect to the MySQL server as the administrative database user root, which is inferred by the use of sudo when running this command. You should see output like this:

```
Output
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 22
Server version: 8.0.19-0ubuntu5 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```
now set the alter user 

```sh
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'mysql@123';
FLUSH PRIVILEGES;
```

# Restarting Apache
```sh
sudo service apache2 restart
```
# Now go to mysql and configure 
# install phpMyAdmin
phpMyAdmin is a free software tool written in PHP, intended to handle the administration of MySQL over the Web. phpMyAdmin supports a wide range of operations on MySQL and MariaDB.

Now Download the phpMyAdmin from an authorized website using wget command
```sh
wget https://files.phpmyadmin.net/phpMyAdmin/4.7.3/phpMyAdmin-4.7.3-all-languages.zip
```
Unzip phpMyAdmin
```sh
unzip phpMyAdmin-4.7.3-all-languages.zip
```
Now rename phpMyAdmin
```sh
mv phpMyAdmin-4.7.3-all-languages phpmyadmin
```
```sh
cd phpmyadmin
```
Here we need to Rename and Edit the configuration file for phpMyAdmin, use these following commands.

```sh
mv config.sample.inc.php config.inc.php
```
Open the config.inc.php and Save file and Close.
```sh
sudo nano config.inc.php
```
now restart apache server 
```sh
sudo service apache2 restart
```
hit the url in browser
```sh
http://localhost/phpMyAdmin
```
