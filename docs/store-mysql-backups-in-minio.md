# Store MySQL Backups in Minio Server [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/minio/minio?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

In this recipe we will learn how to store MySQL backups in Minio Server.

 
## 1. Prerequisites

* Install mc from [here](https://docs.minio.io/docs/minio-client-quickstart-guide).
* Install Minio Server from [here](https://docs.minio.io/docs/minio ).
* Know where the MySQL backups reside in the local filesystem.

## 2. Recipe Steps

Access credentials shown in this example belong to https://play.minio.io:9000.
These credentials are open to public. Feel free to use this service for testing and development. Replace with your own Minio keys in deployment.

### Step 1: Create a bucket.

```sh

$ mc mb play/mysqlbkp
Bucket created successfully ‘play/mysqlbkp’.

```

### Step 2: Mirror mysqlbkup directory where the backup files reside to Minio server. 

```sh

$ mc mirror mysqlbkp/ play/mysqlbkp

```

## 3. Automate

The above recipe can be automated easily. Change the bash script below to your own directories and PATHS as needed. Set up a cron to run this task as needed.

```sh

#!/bin/bash
# Filename: minio-mysql-bkp.sh & has executable permissions.

LOCAL_BACKUP_PATH="/home/miniouser/mysqlbkp"
MINIO_BUCKET="play/mysqlbkp"
MC_PATH="/home/miniouser/go/bin/mc"

$MC_PATH - -quiet mirror $LOCAL_BACKUP_PATH $MINIO_BUCKET

```
