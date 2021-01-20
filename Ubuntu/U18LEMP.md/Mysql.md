Now that you have a web server, you need to install MySQL (a database management system) to store and manage the data for your site.

Install MySQL by typing:

    sudo apt install mysql-server

The MySQL database software is now installed, but its configuration is not yet complete.

To secure the installation, MySQL comes with a script that will ask whether we want to modify some insecure defaults. Initiate the script by typing:

    sudo mysql_secure_installation

This script will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

Warning: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. This will cause issues if you use a weak password in conjunction with software which automatically configures MySQL user credentials, such as the Ubuntu packages for phpMyAdmin. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer Y for yes, or anything else to continue without enabling.

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:

If you’ve enabled validation, the script will also ask you to select a level of password validation. Keep in mind that if you enter 2 – for the strongest level – you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1

Next, you’ll be asked to submit and confirm a root password:

Please set the password for root here.

New password:

Re-enter new password:

For the rest of the questions, you should press Y and hit the ENTER key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes we have made.

Note that in Ubuntu systems running MySQL 5.7 (and later versions), the root MySQL user is set to authenticate using the auth_socket plugin by default rather than with a password. This allows for some greater security and usability in many cases, but it can also complicate things when you need to allow an external program (e.g., phpMyAdmin) to access the user.

If using the auth_socket plugin to access MySQL fits with your workflow, you can proceed to Step 3. If, however, you prefer to use a password when connecting to MySQL as root, you will need to switch its authentication method from auth_socket to mysql_native_password. To do this, open up the MySQL prompt from your terminal:

    sudo mysql



Next, check which authentication method each of your MySQL user accounts use with the following command:

    SELECT user,authentication_string,plugin,host FROM mysql.user;



Output
+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             |                                           | auth_socket           | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
4 rows in set (0.00 sec)

In this example, you can see that the root user does in fact authenticate using the auth_socket plugin. To configure the root account to authenticate with a password, run the following ALTER USER command. Be sure to change password to a strong password of your choosing:

    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';



Then, run FLUSH PRIVILEGES which tells the server to reload the grant tables and put your new changes into effect:

    FLUSH PRIVILEGES;



Check the authentication methods employed by each of your users again to confirm that root no longer authenticates using the auth_socket plugin:

    SELECT user,authentication_string,plugin,host FROM mysql.user;



Output
+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             | *3636DACC8616D997782ADD0839F92C1571D6D78F | mysql_native_password | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
4 rows in set (0.00 sec)

You can see in this example output that the root MySQL user now authenticates using a password. Once you confirm this on your own server, you can exit the MySQL shell:

    exit



Note: After configuring your root MySQL user to authenticate with a password, you’ll no longer be able to access MySQL with the sudo mysql command used previously. Instead, you must run the following:

    mysql -u root -p



After entering the password you just set, you will see the MySQL prompt.

At this point, your database system is now set up and you can move on to installing PHP.
