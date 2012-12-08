=============================
7  Get
=============================

.. contents::


概述
--------------------

Zabbix get用于连接Zabbix agent并从agent上检索需要的信息.

该工具常用于对Zabbix agent进行troubleshooting.

运行Zabbix get
---------------------

在UNIX平台上运行Zabbix get 获得指定的agent上的进程负载::

   shell> cd bin
   shell> ./zabbix_get -s 127.0.0.1 -p 10050 -k "system.cpu.load[all,avg1]"
   
Zabbix get支持以下命令行参数::

   -s --host <主机名或IP>                  指定agent所在的主机或IP地址
   -p --port <端口号>                      指定主机所运行的agent的端口号，默认为10050
   -I --source-address <IP地址>            指定源IP地址
   -k --key <item key>                     指定需要检索的监控项键名
   -h --help                               显示本帮助
   -V --version                            显示版本号
   
在Windows平台下运行Zabbix get类似::

   zabbix_get.exe [options]