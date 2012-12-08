=============================
3  Agent
=============================

.. contents::


概述
--------------------

Zabbix agent部署在被监控机器上用来监控本地资源和应用（如硬盘、内存、处理器统计等）.

Zabbix agent聚合本地的运行信息并将数据发送给Zabbix server以进一步处理. 一旦出现异常(如硬盘空间满的情况或者服务进行宕掉), Zabbix server将会发送告警给管理员报告本次异常.

Zabbix agent利用本地系统调用完成统计信息收集，因此它非常的高效.

   **被动(passive)和主动(active)检查**
   
   Zabbix agent提供被动和主动检查方式.
   
   在 `被动检查` 模式中agent应答数据请求，Zabbix server或者proxy询问agent数据,如CPU load, 然后Zabbix agent回送结果给server.

   `主动检查` 处理过程将相对复杂. agent必须首先进行一次请求Zabbix server索取监控项列表，然后发送对应的值给server.

   选择是被动还是主动检查，需要在 `监控项类型` 中选择'Zabbix agent'或者'Zabbix agent (active)'.


支持的平台
------------------------------

Zabbix agent支持以下平台:

   * Linux
   * IBM AIX
   * FreeBSD
   * NetBSD
   * OpenBSD
   * HP-UX
   * Mac OS X
   * Solaris
   * Windows: 2000, Server 2003, XP, Vista, Server 2008, 7
   
   **安装**
   
   安装相关信息请查看 `安装说明` 相关章节.
   
   
UNIX平台Agent进程(独立守护进程)
--------------------------------

Zabbix agent运行在被监控主机上，可以通过守护进行的方式运行.

运行Zabbix agent,通过以下命令::

   shell> cd sbin
   shell> ./zabbix_agentd
   
运行Zabbix agent时可以指定如下命令行参数::

   -c --config <file>                 指定配置文件，默认的为 /etc/zabbix/zabbix_agentd.conf
   -h --help                          显示本帮助
   -V --version                       显示agent版本号
   -p --print                         显示已知的监控项并退出
   -t --test <item key>               测试指定的监控项并退出
   
例如想查询帮助信息，可以执行::

   shell> zabbix_agentd -h
   
命令行参数的例子如::
   
   shell> zabbix_agentd -c /usr/local/etc/zabbix_agentd.conf
   shell> zabbix_agentd --help
   shell> zabbix_agentd --print
   shell> zabbix_agentd -t "system.cpu.load[all,avg1]"
   
**运行用户**

Zabbix agent设计运行在非root账户下，因此它可以完美运行在启动时的非root账户.
   
如果你在'root'账户下启动Zabbix agent，它将自动选择在操作系统中建立的'zabbix'用户,除非你修改agent配置文件中'AllowRoot'参数。
   
**配置文件**

对于zabbix_agentd的配置详细描述请查看 `配置文件` 章节.


在Windows上运行agent
--------------------------------------

安装方法请查看 `安装Windows agent` 章节.

运行agent服务可以使用控制面板或者运行::

   zabbix_agentd.exe --start
   
命令行语法有::

   zabbix_agentd.exe [-Vhp] [-idsx] [-c <file>] [-t <metric>]
   
可以在Zabbix windows agent命令行使用的选项如下::

   -c --config <file>                       指定配置文件(默认为c:\zabbix_agentd.conf)
   -h --help                                显示帮助信息
   -V --version                             显示版本号
   -p --print                               显示已知的监控项并退出
   -t --test <item key>                     显示指定的监控项并退出
   
功能方法如下::

   -i --install              作为服务安装Zabbix agent
   -d --uninstall            卸载Zabbix agent服务
   -s --start                启动Zabbix agent服务
   -x --stop                 关闭Zabbix agent服务
   
**配置文件**

   Zabbix Windows agent配置文件选项请查看 `配置文件` 章节.
   