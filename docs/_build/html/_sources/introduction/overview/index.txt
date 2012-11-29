==========================
4. Zabbix概述
==========================

架构
---------------
Zabbix主流软件包中包含如下组件

Server
^^^^^^^^^^^^^^^^^^^^

Zabbix Server为中心组件，用来获取agent存活状况及监控数据和统计.  所有的配置、统计、操作数据均通过Server进行存取.

数据库
^^^^^^^^^^^^^^^^^^^^

所有的Zabbix数据均存储在数据库中

Web接口
^^^^^^^^^^^^^^^^^^^^^^^^^^^
为了更简单的无障碍的访问Zabbix, 所以提供了web接口. 该接口作为Zabbix Server的一部分，通常(也有技术控不这样做)和server运行在同一台主机上.

.. warning::

   如果采用SQLite作为数据库，web接口和Zabbix Server必须运行在同一台主机上
   
Proxy
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Zabbix Proxy能够代替Zabbix Server进行性能及可用性数据采集. Proxy是Zabbix部署的可选组件。 如果想分担单一Zabbix Server负载，推荐使用proxy.

Agent
^^^^^^^^^^^^^^^^^^^^^^^^
Zabbix agents 部署在目标监控机上并监控本地资源和应用，将收集数据汇报给Zabbix Server


数据流
---------------------------

In addition it is important to take a step back and have a look at the overall data flow within Zabbix. In order to create an item that gathers data you must first create a host. Moving to the other end of the Zabbix spectrum you must first have an item to create a trigger. You must have a trigger to create an action. Thus if you want to receive an alert that your CPU load it too high on Server X you must first create a host entry for Server X followed by an item for monitoring its CPU, then a trigger which activates if the CPU is too high, followed by an action which sends you an email. While that may seem like a lot of steps, with the use of templating it really isn't. However, due to this design it is possible to create a very flexible setup.
