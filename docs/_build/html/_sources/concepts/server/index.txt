=================
2 Server
=================

概述
================

Zabbix server是Zabbix软件的中心进程.

Server执行polling和trapping来采集数据，评估是否触发触发器，发送报警给用户. 它左右Zabbix agent和proxy的用来报告可用性和一致性数据的中心组件(译者注：好像翻译的部队，还是附上原文吧
It is the central component to which Zabbix agents and proxies report data on availability and integrity of systems.)，Server也可以通过简单服务检查(simple service check)来完成远程网络服务检测.

Server是所有配置、统计和操作数据的中心存储仓库，也是在所有的监控系统中扮演故障发生时通知管理员的角色.

基础Zabbix server依据功能不同划分为三个部分，分别为:Zabbix server、web前端及数据库.

由于Zabbix的所有的配置信息保存在数据库中，server和web前端可以直接进行操作。比如，通过web前端(或者API)创建一个新的监控项时，它将创建的数据插入数据库。一分钟左右Zabbix server会查询监控项数据表，并将查询的监控项
列表保存在自己的缓存(cache)中。这也是为什么通过Zabbix前端进行的变更将在两分钟左右生效.

Server进程
===============

Zabbix server以守护(daemon)进程方式运行，server可以通过以下命令启动::

   shell> cd sbin
   shell> ./zabbix_server
   
你也可以在启动Zabbix server时使用下面的命令行参数::

   -c --config <file>               配置文件的绝对路径(默认是 /etc/zabbix/zabbix_server.conf)
   -n --new-nodeid <nodeid>         转换数据库，使用新的节点id
   -R --runtime-control <option>    运行管理命令
   -h --help                        显示本帮助
   -V --version                     显示版本号
   
.. warning::
   
   在 OpenBSD和NetBSD系统中，Runtime-control不被支持.
   
命令行参数例子如::
   
   shell> zabbix_server -c /usr/local/etc/zabbix_server.conf
   shell> zabbix_server --help
   shell> zabbix_server -V
   
**Runtime control**

Runtime control选项有:

=====================  ==========================================================
选项                   描述
=====================  ==========================================================
config_cache_reload    重载配置缓存，如果配置缓存正在被加载中，将会忽略执行
=====================  ==========================================================

例如使用runtime contorl去重载server配置缓存::
 
   shell> zabbix_server -c /usr/local/etc/zabbix_server.conf -R config_cache_reload
   
**进程账户**

Zabbix设计运行在非root账户下。它可以运行在任何非root账户下。因此你可以运行Zabbix server在非root账户而不无需担心有问题.

如果你想让server运行在'root'下，你必须在系统中调整已经默认写死的'zabbix'用户.

These settings currently cannot be user configured, neither during compilation nor in the configuration file.

如果Zabbix server和agent运行在同一台机器上，建议分别运行在不同的用户下，因为一旦运行的同一个用户下，agent将可以访问server的配置文件，并且能够轻松取得Zabbix Admin级别用户，例如，数据库密码

**配置文件**

请查询zabbix_server配置文件小节以获取详细信息

**启动脚本**

该类脚本用于在系统启动/关闭时自动启动/关闭zabbix进程，位于misc/init.d目录下.

**支持平台**

Due to the security requirements and mission-critical nature of server operation, UNIX is the only operating system that can consistently deliver the necessary performance, fault tolerance and resilience. Zabbix operates on market leading versions.

Zabbix server在以下平台进行过测试:
   
   * Linux
   * Solaris
   * AIX
   * HP-UX
   * Mac OS X
   * FreeBSD
   * OpenBSD
   * NetBSD
   * SCO Open Server
   * Tru64/OSF1
   
 .. note::
   
   Zabbix也许也可以在其他类Unix操作系统中运行良好
   
(linking to other sections, like zabbix maintenance etc)
   
