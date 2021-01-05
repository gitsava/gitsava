# PHP - Scripting Language

PHP is a general-purpose scripting language suited for Web development. PHP scripts can be embedded into HTML. This section explains how to install and configure PHP in an Ubuntu System with Apache2 and MySQL.

This section assumes you have installed and configured Apache2 Web Server and MySQL Database Server. You can refer to the Apache2 and MySQL sections in this document to install and configure Apache2 and MySQL respectively.
## Installation

PHP is available in Ubuntu Linux. Unlike Python, which is installed in the base system, PHP must be added.

To install PHP and the Apache PHP module you can enter the following command at a terminal prompt:
```
sudo apt install php libapache2-mod-php
```
You can run PHP scripts at a terminal prompt. To run PHP scripts at a terminal prompt you should install the php-cli package. To install php-cli you can enter the following command:
```
sudo apt install php-cli
```
You can also execute PHP scripts without installing the Apache PHP module. To accomplish this, you should install the php-cgi package via this command:
```
sudo apt install php-cgi
```
To use MySQL with PHP you should install the php-mysql package, like so:
```
sudo apt install php-mysql
```
Similarly, to use PostgreSQL with PHP you should install the php-pgsql package:
```
sudo apt install php-pgsql
```
## Configuration

If you have installed the libapache2-mod-php or php-cgi packages, you can run PHP scripts from your web browser. If you have installed the php-cli package, you can run PHP scripts at a terminal prompt.

By default, when libapache2-mod-php is installed, the Apache 2 Web server is configured to run PHP scripts using this module. Please verify if the files /etc/apache2/mods-enabled/php7.*.conf and /etc/apache2/mods-enabled/php7.*.load exist. If they do not exist, you can enable the module using the a2enmod command.

Once you have installed the PHP related packages and enabled the Apache PHP module, you should restart the Apache2 Web server to run PHP scripts, by running the following command:
```
sudo systemctl restart apache2.service
```
Testing

To verify your installation, you can run the following PHP phpinfo script:
```
<?php
  phpinfo();
?>
```
You can save the content in a file phpinfo.php and place it under the DocumentRoot directory of the Apache2 Web server. Pointing your browser to http://hostname/phpinfo.php will display the values of various PHP configuration parameters.
References

    For more in depth information see the php.net documentation.

    There are a plethora of books on PHP. A good book from O’Reilly is Learning PHP, which includes an exploration of PHP 7’s enhancements to the language. PHP Cook Book, 3rd Edition is also good, but has not yet been updated for PHP 7.

    Also, see the Apache MySQL PHP Ubuntu Wiki page for more information.
