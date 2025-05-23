---
title: "Setting Up Master Slave Replication in Postgresql Using Dockers and External Volumes"
meta_title: "Setting Up Master Slave Replication in Postgresql Using Dockers and External Volumes"
description: "Setting Up Master Slave Replication in Postgresql Using Dockers and External Volumes"
date: 2021-09-11T13:34:03+05:30
author: "Rishabh"
categories: ["Postgresql","technology"]
tags: ["Postgresql","technology"]
draft: false
---


## Understanding replication in PostgreSQL 12

Streaming replication in PostgreSQL works on log shipping. Every transaction in postgres is written to a transaction log called WAL (write-ahead log) to achieve durability. A slave uses these WAL segments to continuously replicate changes from its master.

There exists three mandatory processes – wal sender , wal receiver and startup process, these play a major role in achieving streaming replication in postgres.

A wal sender process runs on a master, whereas the wal receiver and startup processes runs on its slave. When you start the replication, a wal receiver process sends the LSN (Log Sequence Number) up until when the WAL data has been replayed on a slave, to the master. And then the wal sender process on master sends the WAL data until the latest LSN starting from the LSN sent by the wal receiver, to the slave. Wal receiver writes the WAL data sent by wal sender to WAL segments. It is the startup process on slave that replays the data written to WAL segment. And then the streaming replication begins.

Note: Log Sequence Number, or LSN, is a pointer to a location in the WAL.

## Firewall
UFW or Uncomplicated Firewall is an application to manage the iptables based firewall on Ubuntu. UFW is the default firewall configuration tool for Ubuntu Linux and provides a user-friendly way to configure the firewall.

```shell
apt-get install -y ufw
```

Add new services to the UFW firewall: add SSH and PostgreSQL services with commands below.

```shell
ufw allow ssh
ufw allow postgresql
```

Enable the UFW firewall and check the status.

```shell
ufw enable
ufw status
```

UFW firewall has been installed and the PostgreSQL service has been added.

## Setting up Docker using external volume

### Install docker
You can install docker from your default package manager or using some other service like [**Snapcraft**](https://snapcraft.io/) e.g. ``snap install docker``

### Setup Docker engine
#### Pull postgress in docker

```shell
docker pull postgres
```

#### Create docker

```shell
docker run --name DOCKER_NAME -e POSTGRES_PASSWORD=PASSWORD -d -p 0.0.0.0:5432:5432 -v /mnt/EXTERNAL_VOLUME_NAME/postgres:/var/lib/postgresql/data  postgres
```

### Check for running dockers

```shell
docker ps
```

### View all available dockers

```shell
docker ps -a
```

### Enter into Docker shell

```shell
docker exec -it DOCKER_NAME /bin/bash
```

## Master -
Create a role dedicated to the replication -
Create the user in master using whichever slave should connect for streaming the WALs. This user must have REPLICATION ROLE.

```shell
CREATE USER replica REPLICATION LOGIN ENCRYPTED PASSWORD 'STRONG_PASSWORD_HERE';
```

Now check the new user with 'du' query below, and you will see the replica user with replication privileges.

```shell
\du
```

### Edit postgresql.conf
Note - the postgresql.conf would be present in the following location in case of external volume
```shell
/mnt/EXTERNAL_VOLUME_NAME/postgres/postgresql.conf
```

The following parameters on the master are considered as mandatory when setting up streaming replication:

* **archive_mode** : Must be set to ON to enable archiving of WALs.

* **wal_level** : Must be at least set to hot_standby  until version 9.5 or replica  in the later versions.

* **max_wal_senders** : Must be set to 3 if you are starting with one slave. For every slave, you may add 2 wal senders.

* **wal_keep_segments** : Set the WAL retention in pg_xlog (until PostgreSQL 9.x) and pg_wal (from PostgreSQL 10). Every WAL requires 16MB of space unless you have explicitly modified the WAL segment size. You may start with 100 or more depending on the space and the amount of WAL that could be generated during a backup.

* **archive_command** : This parameter takes a shell command or external programs. It can be a simple copy command to copy the WAL segments to another location or a script that has the logic to archive the WALs to S3 or a remote backup server.

* **listen_addresses** : Set it to * or the range of IP Addresses that need to be whitelisted to connect to your master PostgreSQL server. Your slave IP should be whitelisted too, else, the slave cannot connect to the master to replicate/replay WALs.

* **hot_standby** : Must be set to ON on standby/replica and has no effect on the master. However, when you setup your replication, parameters set on the master are automatically copied. This parameter is important to enable READS on slave. Otherwise, you cannot run your SELECT queries against slave.

The above parameters can be set on the master using these commands followed by a restart:

```shell
wal_level = replica
max_wal_senders = 3 # max number of walsender processes
wal_keep_segments = 64 # in logfile segments, 16MB each; 0 disables
listen_addresses = '*'
# or listen_address = ‘IP_OF_SERVER’
archive_mode = on
archive_command = 'cp %p /var/lib/postgresql/12/main/archive/%f'
synchronous_commit = local
synchronous_standby_names = 'pgslave001'
```

In the postgresql.conf file, the archive mode is enabled, so we need to create a new directory for the archive. Create a new archive directory, change the permission and change the owner to the postgres user.

```shell
mkdir -p /var/lib/postgresql/12/main/archive/
chmod 700 /var/lib/postgresql/12/main/archive/
chown -R postgres:postgres /var/lib/postgresql/12/main/archive/
```

Create the archive dir in the external storage -
Mount the location on docker configuration file (Docker has permission to read write and execute everything, we are running it through root)

```shell
/mnt/external_volume:/var/lib/postgresql/12/main/archive/
```

### Edit pg_hba.conf

Add an entry to pg_hba.conf of the master to allow replication connections from the slave. The default location of pg_hba.conf is the data directory. However, you may modify the location of this file in the file  postgresql.conf. In Ubuntu/Debian, pg_hba.conf may be located in the same directory as the postgresql.conf file by default. You can get the location of postgresql.conf in Ubuntu/Debian by calling an OS command => pg_lsclusters.

```shell
# Localhost
host    replication     replica          127.0.0.1/32             md5
# PostgreSQL Master IP address
host    replication     replica          10.0.15.10/32            md5
# PostgreSQL SLave IP address
host    replication     replica          10.0.15.11/32            md5
```

Save and exit, then restart PostgreSQL.

```shell
systemctl restart postgresql
```

PostgreSQL is running under the IP address 10.0.15.10, check it with netstat command.

```shell
netstat -plntu
```

## Slave -

First stop the postgresql service using the following command

```shell
systemctl stop postgresql
```

then navigate to the postgresql directory

```shell
cd etc/postgresql/12/main/
```

and then edit the postgresql.conf file

```shell
vim postgresql.conf
```

The following parameters on the slave are considered as mandatory when setting up streaming replication, uncomment these parameters and add the following values to them:

```shell
listen_address = 10.0.15.11
# Note: The IP will be same as that you've already added the ip in the pg_hba.conf file in Master
wal_level = hot_standby
synchronous_commit = local
max_wal_senders = 2
# max_wal_senders is set to 2 because we are using 2 servers (master, slave). Similarly this value can be set to 3 if we use 3 servers.
wal_keep_segments = 10
synchronous_standby_names = 'pgslave001'
hot_standby = on
```

## Starting the Data Streaming

To start stream the data and to bring Slave at the same state as that of Master, we do the following steps:

* Copy the data of Master to Slave

* Create a recovery configuration file

* And restart the postgresql service on Slave

### Copying the data of Master to Slave
Login to Slave and create a backup of the `main/` directory using the following commands

```shell
su - postgres
cd 12/
mv main main-backup
# Creating new main/ directory
mkdir main/
chmod 700 main/
```

Then copy the `main/` directory of Master on Slave using the following commands

```shell
pg_basebackup -h 10.0.15.10 -U replica -D /var/lib/postgresql/12/main -P --xlog
Password:
```

Wait for data transfer to complete and then create a `recovery.conf` file on the Slave

```shell
cd /var/lib/postgresql/9.6/main/
vim recovery.conf
```

and add the following content to it
Note: The `STRONG_PASSWORD_HERE` is same as you've used above in the **Master** section

Explanation of each parameter:

* **standby_mode=on** : specifies that the server must start as a standby server

* **primary_conninfo** : the parameters to use to connect to the master

* **trigger_file** : if this file exists, the server will stop the replication and act as a master

* **restore_command** : this command is only needed if you have used the archive_command on the master

```shell
standby_mode = 'on'
primary_conninfo = 'host=10.0.15.10 port=5432 user=replica password=STRONG_PASSWORD_HERE application_name=pgslave001'
restore_command = 'cp /var/lib/postgresql/12/main/archive/%f %p'
trigger_file = '/tmp/postgresql.trigger.5432'
```

save the file and change it's permission

```shell
chmod 600 recovery.conf
```

now restart postgresql and make sure the service is running

```shell
systemctl start postgresql
netstat -plntu
```

## Testing

One can check the streaming status on Master

```shell
postgres=# select * from pg_stat_activity  where usename = 'replica' ;
application_name |   state   | sync_priority | sync_state
-----------------+-----------+---------------+------------
pgslave001       | streaming |             1 | sync
(1 row)
```

One can check for user `replica` on the Master

```shell
postgres=# select * from pg_stat_activity  where usename = 'replica' ;
-[ RECORD 1 ]----+------------------------------
datid            |
datname          |
pid              | 9134
usesysid         | 16384
usename          | replica
application_name | walreceiver
client_addr      | 172.17.0.3
client_hostname  |
client_port      | 45234
backend_start    | 2020-03-11 19:08:56.049113+00
xact_start       |
query_start      |
state_change     | 2020-03-11 19:08:56.071363+00
wait_event_type  | Activity
wait_event       | WalSenderMain
state            | active
backend_xid      |
backend_xmin     |
query            |
backend_type     | walsender
```

## References
1. [Setting up Master Slave Replication in PostgreSQL using Dockers and external volumes](https://github.com/Rishabh04-02/setting-up-master-slave-replication-in-postgresql-using-dockers-and-external-volumes)
2. [Setting up Master Slave Replication in PostgreSQL (upto version 11) using Dockers and external volumes](https://github.com/Rishabh04-02/Master-Slave-Replication-in-PSQL)
3. [Setting up Streaming Replication Postgresql](https://www.percona.com/blog/2018/09/07/setting-up-streaming-replication-postgresql/)
4. [Postgresql Raveland blog](https://blog.raveland.org/post/postgresql_sr/)
5. [How to set up master slave replication for postgresql](https://www.howtoforge.com/tutorial/how-to-set-up-master-slave-replication-for-postgresql-96-on-ubuntu-1604/)
6. [How to Set Up Streaming Replication in PostgreSQL 12](https://www.percona.com/blog/2019/10/11/how-to-set-up-streaming-replication-in-postgresql-12/)
