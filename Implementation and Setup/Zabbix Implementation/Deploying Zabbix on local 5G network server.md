
### The integration steps are as follows:

Configuration on : ubuntu 20.4 ( New VM installed for Zabbix server installation with IP address as 192.168.64.6 , hostname: zabbix )

### Step 1: 

To provide the web-backed capability for Zabbix Server, first update the software packages and then install Apache Web Server alongside PHP by issuing the following command.

```zabbix@zabbix:-$ sudo apt update / sudo apt upgrade```

Then install apache web server by following command:

```zabbix@zabbix:-$ sudo apt install apache2 php php-mysql php-mysqlnd php-ldap php-bcmath php-mbstring php-gd php-pdo php-xml libapache2-mod-php```

### Step 2:

Now to tune the PHP interpreter, adjust some values in order to run Zabbix Server. So, open Apache php.ini configuration file for editing by
issuing the following command:
```zabbix@zabbix:-$ sudo nano /etc/php/7.X/apache2/php.in```

Changes done in the file are:

```post_max_size= 16M```
```upload_max_filesize= 2M```
```max_execution_time= 300```
```max_input_time= 300```
```memory_limit = 128M```
```session.auto_start= 0```
```mbstring.func_overload= 0```
```date.timezone= America/Toronto```

### Step 3:

Restart the apache2.service:
```zabbix@zabbix: $ sudo systemctl restart apache2.service```

### Step 4:

Setting up the database MariaDB and installing packages:

```zabbix@zabbix: $ sudo apt-get install libmysqlclient-dev```

```zabbix@zabbix: $ sudo apt-get install mariadb-server mariadb-client libmariadbd-dev```

```zabbix@zabbix: $ sudo systemctl start mariadb```

Installation of MariaDB:

```zabbix@zabbix: $ sudo systemctl start mariadb```

```zabbix@zabbix: $ sudo mysql_secure_installation```

### Step 5:

Creating an RDBMS by Logging in to the database component

(MariaDB) and creating a Zabbix database and the credentials required to manage the database by issuing the following commands:

```
zabbix@zabbix: $ sudo mysql -uroot -p
```

Enter password: 

```
MariaDB [(none)]> create database zabbix character set utf8mb4 collate utf8mb4_bin;
```

Query OK, 1 row affected (0.014 sec)

```
MariaDB [(none)]> create user zabbix@localhost identified by ’zabbix’;
```

Query OK, 0 rows affected (0.027 sec)

```
MariaDB [(none)]> grant all privileges on zabbix.* to zabbix@localhost;
```

Query OK, 0 rows affected (0.024 sec)

```
MariaDB [(none)]> quit;
```

### Step 6: 
Zabbix server installation:

The first step is to download the Zabbix repository by the following commands:

```
zabbix@zabbix: $ sudo wget https://repo.zabbix.com/zabbix/6.0/ubuntuarm64/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu20.04_all.deb
```

Using the debian package manager command as below:

```
zabbix@zabbix: $ sudo dpkg -i zabbix-releas_6.0-1+ubuntu20.04_all.deb
```

Installing Zabbix server:

```
zabbix@zabbix: $ sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

Before configuring the server, first, importing Zabbix’s initial database schema to the MySQL database. Importing the schema against the database created for the Zabbix application by issuing the below command:

```
zabbix@zabbix: $ sudo zcat /usr/share/doc/zabbix-sql-scripts/mysql/server.sql.gz | mysql -uzabbix -p zabbix

```
Now, set up the Zabbix server by opening the main configuration file for editing with the following command.

```
zabbix@zabbix: $ sudo nano /etc/zabbix/zabbix_server.conf
```
Changes done in the file are as follows:

```
DBHost= localhost

DBName= zabbixdb

DBUser= zabbixuser

DBPassword= password1

```
Now, restart the Zabbix daemon to apply changes by issuing the below command.

```
zabbix@zabbix: $ sudo systemctl restart zabbix-server.service
```

Configuration of local Zabbix agent is required to monitor the Zabbix server as well, for which we needed to change the Zabbix agent configuration file as below:

```
zabbix@zabbix: $ sudo nano /etc/zabbix/zabbix_agentd.conf

```
Changes required in zabbix_agentd.conf file :

```
Server: 127.0.0.1

Listenport:10050

```
Restarting the Zabbix-agent.service with the below command:

```
zabbix@zabbix: $Systemctl restart zabbix-agent.service
```

# Configuration for zabbix frontend: 

Check the IP address of the Zabbix server machine.
 
In our case it is **(192.168.64.6)** as below:
 
```
zabbix@zabbix: $ ifconfig enp0s10
 
```

