# MySQL

MySQL is a fast, multi-threaded, multi-user, and robust SQL database server. It is intended for mission-critical, heavy-load production systems and mass-deployed software.
## Installation

To install MySQL, run the following command from a terminal prompt:
```
sudo apt install mysql-server
```
Once the installation is complete, the MySQL server should be started automatically. You can quickly check its current status via systemd:
```
sudo service mysql status
```
```
● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2019-10-08 14:37:38 PDT; 2 weeks 5 days ago
 Main PID: 2028 (mysqld)
    Tasks: 28 (limit: 4915)
   CGroup: /system.slice/mysql.service
           └─2028 /usr/sbin/mysqld --daemonize --pid-file=/run/mysqld/mysqld.pid

Oct 08 14:37:36 db.example.org systemd[1]: Starting MySQL Community Server...
Oct 08 14:37:38 db.example.org systemd[1]: Started MySQL Community Server.
````
The network status of the MySQL service can also be checked by running the ss command at the terminal prompt:
```
sudo ss -tap | grep mysql
```
When you run this command, you should see something similar to the following:
```
LISTEN    0         151              127.0.0.1:mysql             0.0.0.0:* users:(("mysqld",pid=149190,fd=29))
LISTEN    0         70                       *:33060                   *:*       users:(("mysqld",pid=149190,fd=32))
```
If the server is not running correctly, you can type the following command to start it:
```
sudo service mysql restart
```
A good starting point for troubleshooting problems is the systemd journal, which can be accessed at the terminal prompt with this command:
```
sudo journalctl -u mysql
```
## Configuration

You can edit the files in /etc/mysql/ to configure the basic settings – log file, port number, etc. For example, to configure MySQL to listen for connections from network hosts, in the file /etc/mysql/mysql.conf.d/mysqld.cnf, change the bind-address directive to the server’s IP address:
```
bind-address            = 192.168.0.5
```
    Note

    Replace 192.168.0.5 with the appropriate address, which can be determined via ip address show.

After making a configuration change, the MySQL daemon will need to be restarted:
```
sudo systemctl restart mysql.service
```
## Database Engines

Whilst the default configuration of MySQL provided by the Ubuntu packages is perfectly functional and performs well there are things you may wish to consider before you proceed.

MySQL is designed to allow data to be stored in different ways. These methods are referred to as either database or storage engines. There are two main engines that you’ll be interested in: InnoDB and MyISAM. Storage engines are transparent to the end user. MySQL will handle things differently under the surface, but regardless of which storage engine is in use, you will interact with the database in the same way.

Each engine has its own advantages and disadvantages.

While it is possible, and may be advantageous to mix and match database engines on a table level, doing so reduces the effectiveness of the performance tuning you can do as you’ll be splitting the resources between two engines instead of dedicating them to one.

    MyISAM is the older of the two. It can be faster than InnoDB under certain circumstances and favours a read only workload. Some web applications have been tuned around MyISAM (though that’s not to imply that they will slow under InnoDB). MyISAM also supports the FULLTEXT data type, which allows very fast searches of large quantities of text data. However MyISAM is only capable of locking an entire table for writing. This means only one process can update a table at a time. As any application that uses the table scales this may prove to be a hindrance. It also lacks journaling, which makes it harder for data to be recovered after a crash. The following link provides some points for consideration about using MyISAM on a production database.

    InnoDB is a more modern database engine, designed to be ACID compliant which guarantees database transactions are processed reliably. Write locking can occur on a row level basis within a table. That means multiple updates can occur on a single table simultaneously. Data caching is also handled in memory within the database engine, allowing caching on a more efficient row level basis rather than file block. To meet ACID compliance all transactions are journaled independently of the main tables. This allows for much more reliable data recovery as data consistency can be checked.

As of MySQL 5.5 InnoDB is the default engine, and is highly recommended over MyISAM unless you have specific need for features unique to the engine.
## Advanced configuration
### Creating a tuned configuration

There are a number of parameters that can be adjusted within MySQL’s configuration files that will allow you to improve the performance of the server over time.

Many of the parameters can be adjusted with the existing database, however some may affect the data layout and thus need more care to apply.

First, if you have existing data, you will need to carry out a mysqldump and reload:
```
mysqldump --all-databases --routines -u root -p > ~/fulldump.sql
```
This will then prompt you for the root password before creating a copy of the data. It is advisable to make sure there are no other users or processes using the database whilst this takes place. Depending on how much data you’ve got in your database, this may take a while. You won’t see anything on the screen during this process.

Once the dump has been completed, shut down MySQL:
```
sudo service mysql stop
```
It’s also a good idea to backup the original configuration:
```
sudo rsync -avz /etc/mysql /root/mysql-backup
```
Next, make any desired configuration changes.

Then delete and re-initialise the database space and make sure ownership is correct before restarting MySQL:
```
sudo rm -rf /var/lib/mysql/*
sudo mysqld --initialize
sudo chown -R mysql: /var/lib/mysql
sudo service mysql start
```
The final step is re-importation of your data by piping your SQL commands to the database.
```
cat ~/fulldump.sql | mysql
```
For large data imports, the ‘Pipe Viewer’ utility can be useful to track import progress. Ignore any ETA times produced by pv, they’re based on the average time taken to handle each row of the file, but the speed of inserting can vary wildly from row to row with mysqldumps:
```
sudo apt install pv
pv ~/fulldump.sql | mysql
```
Once that is complete all is good to go!

    Note

    This is not necessary for all my.cnf changes. Most of the variables you may wish to change to improve performance are adjustable even whilst the server is running. As with anything, make sure to have a good backup copy of config files and data before making changes.

## MySQL Tuner

MySQL Tuner connects to a running MySQL instance and offer configuration suggestions to optimize the database for your workload. The longer the server has been running, the better the advice mysqltuner can provide. In a production environment, consider waiting for at least 24 hours before running the tool. You can install mysqltuner from the Ubuntu repositories:
```
sudo apt install mysqltuner
```
Then once its been installed, run:
```
mysqltuner
```
and wait for its final report. The top section provides general information about the database server, and the bottom section provides tuning suggestions to alter in your my.cnf. Most of these can be altered live on the server without restarting; look through the official MySQL documentation (link in Resources section) for the relevant variables to change in production. The following example is part of a report from a production database showing potential benefits from increasing the query cache:

-------- Recommendations -----------------------------------------------------
General recommendations:
    Run OPTIMIZE TABLE to defragment tables for better performance
    Increase table_cache gradually to avoid file descriptor limits
Variables to adjust:
    key_buffer_size (> 1.4G)
    query_cache_size (> 32M)
    table_cache (> 64)
    innodb_buffer_pool_size (>= 22G)

It goes without saying that performance optimization strategies vary from application to application. So for example, what works best for Wordpress might not be the best for Drupal or Joomla. Performance can be dependent on the types of queries, use of indexes, how efficient the database design is and so on. You may find it useful to spend some time searching for database tuning tips based on what applications you’re using. Once you’ve reached the point of diminishing returns from database configuration adjustments, look to the application itself for improvements, or invest in more powerful hardware and/or scaling up the database environment.
