# Dump

Restore

```
mysql -p -u[user] [database] < db_backup.dump
```

Dump

```
mysqldump --all-databases > backup-180421.sql
```

# Drop database / Clear database

```
DROP DATABASE blafoo;
CREATE DATABSE blafoo;
```

## Galera

### Monitor Cluster Status

http://galeracluster.com/documentation-webpages/monitoringthecluster.html

```
mysql -u root -p<your_password> --exec="SHOW STATUS LIKE 'wsrep%';"
```

## Backup

Kolla Backup Blueprint
https://blueprints.launchpad.net/kolla/+spec/database-backup-recovery

http://galeracluster.com/documentation-webpages/backingupthecluster.html
https://severalnines.com/blog/full-restore-mysql-galera-cluster-backup
https://severalnines.com/blog/deploy-asynchronous-replication-slave-mariadb-galera-cluster-gtid-clustercontrol

http://galeracluster.com/documentation-webpages/sst.html

# Mysql bin log

http://www.pc-erfahrung.de/sonstiges/webdesignwebentwicklung/mysql-binary-log-erklaerung-deaktivieren-und-loeschen.html
