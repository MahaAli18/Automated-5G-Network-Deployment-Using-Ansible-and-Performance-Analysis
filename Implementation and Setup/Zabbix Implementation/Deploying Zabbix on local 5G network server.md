
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

