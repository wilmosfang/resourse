# import the data to influxdb


## cli

~~~
git clone https://github.com/wilmosfang/resourse.git
influxd restore -portable -db new_test resourse/grafana/influxdb.new_test
~~~

## log

~~~
[root@influxdb tmp]# git clone https://github.com/wilmosfang/resourse.git
Cloning into 'resourse'...
remote: Enumerating objects: 20, done.
remote: Counting objects: 100% (20/20), done.
remote: Compressing objects: 100% (16/16), done.
remote: Total 20 (delta 1), reused 20 (delta 1), pack-reused 0
Unpacking objects: 100% (20/20), done.
[root@influxdb tmp]#
[root@influxdb tmp]# ll resourse/grafana/influxdb.new_test
total 724
-rw-rw-r--. 1 root root    484 Aug 23 15:43 20190823T152249Z.manifest
-rw-rw-r--. 1 root root    542 Aug 23 15:43 20190823T152249Z.meta
-rw-rw-r--. 1 root root 661688 Aug 23 15:43 20190823T152249Z.s25.tar.gz
-rw-rw-r--. 1 root root  68588 Aug 23 15:43 20190823T152249Z.s26.tar.gz
[root@influxdb tmp]# 
[root@influxdb tmp]# influx
Connected to http://localhost:8086 version 1.7.7
InfluxDB shell version: 1.7.7
> show databases
name: databases
name
----
_internal
grafana_test
new_test
abc_test
> drop database new_test;
> show databases
name: databases
name
----
_internal
grafana_test
abc_test
> exit
[root@influxdb tmp]#
[root@influxdb tmp]# influxd restore -portable -db new_test resourse/grafana/influxdb.new_test
2019/08/23 15:47:55 Restoring shard 25 live from backup 20190823T152249Z.s25.tar.gz
2019/08/23 15:47:55 Restoring shard 26 live from backup 20190823T152249Z.s26.tar.gz
[root@influxdb tmp]# 
[root@influxdb tmp]# influx
Connected to http://localhost:8086 version 1.7.7
InfluxDB shell version: 1.7.7
> show databases;
name: databases
name
----
_internal
grafana_test
abc_test
new_test
> use new_test;
Using database new_test
> select count(*) from data;
name: data
time count_value
---- -----------
0    604800
> select * from data limit 10;
name: data
time                city     geohash      ip              value
----                ----     -------      --              -----
1563810069000000000 Xinfeng  wsfdhrpbfc5p 114.114.114.114 141
1563810070000000000 Xinfeng  wsfdhrpbfc5p 114.114.115.115 26
1563810071000000000 Hangzhou wtmkq6fck1dg 223.5.5.5       55
1563810072000000000 Hangzhou wtmkq6fck1dg 223.6.6.6       111
1563810073000000000 Beijing  wx4g08vyh16v 180.76.76.76    71
1563810074000000000 Beijing  wx4g08vyh16v 119.29.29.29    143
1563810075000000000 Shenzhen ws1078mcrcpz 182.254.116.116 48
1563810076000000000 Beijing  wx4g08vyh16v 1.2.4.8         98
1563810077000000000 Beijing  wx4g08vyh16v 210.2.4.8       72
1563810078000000000 Shanghai wtw3egg49gw9 117.50.11.11    107
> exit
[root@influxdb tmp]# 
~~~



