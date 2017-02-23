---
title: "What I learned with a big database"
date: 2017-01-15T15:12:23+01:00
comments: true
categories: [development]
---
So I recently started a new side project that involves data mining. While working on this project I've learned a little bit about how to manage a larger than usual database. At the point of writing this the database is approximately 50GB and growing daily. So here are a few things I've learned.

<!-- more -->

# Backups

This is probably the main area where I learned a bunch of stuff. Usually when you're dealing with a database of approximately 1GB in size, backups at midnight are rather routine. You run mysqldump and you're done. However when your database gets larger and is constantly being used this suddenly becomes an actual task.

## Table locks

My original attempts to do mysqldump resulted in all my miners being unable to insert into the database. It turns out by default mysqldump locks all the tables. This becomes an issue when mysqldump takes 1+ hours to run. However you can use the `--single-transaction` flag to make the mysqldump to start a transaction and use this for all the reads. That means the writes can continue while you're doing a mysqldump.

## Compression

When running mysqldump I was creating the SQL file and then after that compressing it before transferring it to S3 for storage. This turns out isn't the best approach as the reading and writing to the same disk can cause a slow down in the speed of the dump. You can reduce this by piping mysqldump's output into a compression application directly. That way you're writing less data to disk so your mysqldump isn't waiting for disk io.

I also found out that gzip still only uses one core by default. However someone nicely wrote an upgraded version that uses all cores, it's called pigz. You can also use this with tar.

## Xtrabackup

After a while I realised that mysqldump wasn't the best choice for a backup when dealing with a 50+GB database. So I started looking into other methods. I ended up using Percona XtraBackup. This works by copying the innodb files instead of creating a sql file. You also need to use it to restore your backups. This performed almost 4 times faster than mysqldump.

One of the parts of the backup process is applying the innodb logs that haven't been executed yet. By default this took 12+ hours before I killed it. It turns out that it has a `--use-memory` flag. By default it only uses very little memory. I've upped this to 7GB and it flew by in comparison.

# Tuning

Considering my database is extremely write heavy at the moment (99% writes 1% reads). It turned out I need to improve the performance of my writes. I did this by tuning the MySQL settings.

The two main settings I changed were: innodb_buffer_pool_size and innodb_log_file_size. This resulted in skyrocketing my write performance in comparison to what I was getting.

# Replication

I found out that if I want to do any actual work on the data I've mined that I would have to create a master-slave replication setup. To avoid locking the tables and slowing down/killing my crawlers.
