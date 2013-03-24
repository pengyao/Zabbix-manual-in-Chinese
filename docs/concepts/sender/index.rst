=============================
6  Sender
=============================

.. contents::


概述
--------------------

Zabbix sender命令行工具常用于发送性能数据给Zabbix server.

该工具常用于在长时间运行的用户自定义脚本中以便不断发送可用性及性能数据.


运行Zabbix sender
----------------------------

在UNIX下运行Zabbix sender的例子::

   shell> cd bin
   shell> ./zabbix_sender -z zabbix -s "Linux DB3" -k db.connections -o 43
   
参数的对应说明:

   * z  -  指定Zabbix server主机(常用IP地址)
   * s  -  监控主机名称(在Zabbix前段中填写的主机名)
   * k  -  监控项键名
   * o  -  需要发送的值
   
查看 `Zabbix sender manpage <http://www.zabbix.com/documentation/1.8/manpages/zabbix_sender>`_ 获取更多内容.

不管是在类UNIX系统还是Windows中, Zabbix sender接受UTF-8字符串.

在Windows平台，可以同样运行::

   zabbix_sender.exe [options]
   
Since Zabbix 1.8.4, zabbix_sender realtime sending scenarios have been improved to gather multiple values passed to it in close succession and send them to the server in a single connection. A value that is not further apart from the previous value than 0.2 seconds can be put in the same stack, but maximum pooling time still is 1 second.

如果想通过输入文件发送多个值。 Zabbix sender将会以250个值为一组进行一次发送(所有的值都会被处理),例如::

   # zabbix_sender -z 127.0.0.1 -i /tmp/traptest.txt
   Info from server: "Processed 250 Failed 0 Total 250 Seconds spent 0.002668"
   Info from server: "Processed 50 Failed 0 Total 50 Seconds spent 0.000540"
   sent: 300; skipped: 0; total: 300
   
所有的输入文件的条目都将按照从上到下的顺序进行发送.

如果有触发器关联到这些监控项，输入文件中所有的时间戳必须按照自增的顺序进行排列，否则会导致事件(event)计算错误.

   .. warning::
   
      如果指定的配置文件中参数条目无效(并非按照 参数=值 的方式)，Zabbix sender将会终止运行 (译者注：此处的配置文件不太懂指的是什么意思)
	  
	  

