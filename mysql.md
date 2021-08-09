```
apt install mysql-server
mysql_secure_installation
mysql -u root -p
CREATE USER 'mohsen'@'host' IDENTIFIED BY '1177786mM';
```

#### Replicate

```
nano /etc/mysql/mysql.conf.d/mysqld.cnf
CREATE USER rpl_user@138.201.101.50 IDENTIFIED BY '1177786mM';
ALTER USER rpl_user@138.201.101.50 IDENTIFIED WITH mysql_native_password BY '1177786mM';
grant replication slave on *.* to rpl_user@138.201.101.50;
flush privileges;
show grants for rpl_user@138.201.101.50;

CHANGE MASTER TO MASTER_HOST='92.119.57.160',
MASTER_USER='rpl_user',
MASTER_PASSWORD='1177786mM',
MASTER_LOG_FILE='mysql-bin.000002',
MASTER_LOG_POS=1588775;

SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 2;
CHANGE MASTER TO MASTER_SSL = 0
```

