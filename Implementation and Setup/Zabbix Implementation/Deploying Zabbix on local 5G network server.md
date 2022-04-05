
### The integration steps are as follows:

Configuration on : ubuntu 20.4 ( New VM installed for Zabbix server installation with IP address as 192.168.64.6 , hostname: zabbix )

### Step 1: 

To provide the web-backed capability for Zabbix Server, first update the software packages and then install Apache Web Server alongside PHP by issuing the following command.

```zabbix@zabbix:-$ sudo apt update / sudo apt upgrade```

Then install apache web server by following command:

```zabbix@zabbix:-$ sudo apt install apache2 php php-mysql php-mysqlnd php-ldap php-bcmath php-mbstring php-gd php-pdo php-xml libapache2-mod-php```
