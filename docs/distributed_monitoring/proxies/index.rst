================================
1 代理
================================

.. contents::

概述
--------------------------

Zabbix代理能够取代Zabbix server去收集性能和可行用数据. 因此代理常用于完成Zabbix server数据收集工作并降低server负载.

同时，使用代理也是在集中和分布式监控中最简单的实现方案，所有的agent和代理数据将发送给一个Zabbix server,所有数据集中存储.

Zabbix代理常用于以下场景:

   * 监控远程区域
   * Monitor locations having unreliable communications
   * 当监控成千上万设备时，采用代理有效降低Zabbix server负载
   * 易于维护的分布式监控场景
   
.. image:: /_static/images/proxy.png

代理和Zabbix server通信采用TCP连接，因此你只需要配置一条防火墙规则即可.

   .. warning::
   
      Zabbix代理必须使用独立的数据库，否则指向Zabbix server数据库将损坏配置.
	  
在将数据发送给server之前，所有的数据都会存储在代理本地. 用这种策略是为了防止server出现问题时丢失数据. 代理配置文件中参数 *ProxyLocalBuffer* 和 *ProxyOffineBuffer* 用来控制数据保存在本地多久.

Zabbix代理是一个数据收集器.它不含有触发器,事件和发送告警功能. 下表将列出来代理的功能:

============================   ======================
功能                           代理是否支持本功能
============================   ======================   
Zabbix agent check             **Yes**
Zabbix agent checks(active)    **Yes**
Simple checks                  **Yes**
Trapper items                  **Yes**
SNMP checks                    **Yes**
SNMP traps                     **Yes**
IPMI checks                    **Yes**
JMX checks                     **Yes**
Log file monitoring            **Yes**
Internal checks                No
SSH checks                     **Yes**
Telnet checks                  **Yes**
External checks                **Yes**
Built-in web monitoring        **Yes**
Network discovery              **Yes**
Low-level discovery            **Yes**
Calculating triggers           No
Processing events              No
Sending alerts                 No
Remote commands                No
============================   ======================

   .. warning::
      
      为确保agent可以询问代理进行active checks,代理必须存在于agent的配置文中的 **ServerActive** 参数中.

配置
--------------------------

一旦你安装和配置成功代理，是时候完成Zabbix前端的配置了.

**添加代理**

在Zabbix前端中配置代理::

   *前往 `Administration` -> `DM`
   *在右上角的下拉框中选择 `Proxies`
   *点击 `Create proxy` 或者点击已存在的代理名称

.. image:: /_static/images/distributed_monitoring/proxy.png


+--------------------+------------------------------------------------------------------------------+
|参数                |描述                                                                          |
+====================+==============================================================================+
|`Proxy name`        |输入代理名称. 该值必须和代理配置文件中的 **Hostname** 参数内容相同            |
+--------------------+------------------------------------------------------------------------------+
|`Proxy mode`        | 选择代理方式                                                                 |
|                    | **Active** - 代理将主动连接Zabbix server请求配置数据                         |
|                    | **Passive** - Zabbix server连接代理                                          |
+--------------------+------------------------------------------------------------------------------+
|`Hosts`             |选择需要通过本代理进行监控的主机                                              |
+--------------------+------------------------------------------------------------------------------+

**主机配置**

你也可以在主机配置表单中选择代理,使用 **Monitored by proxy** 

.. image:: /_static/images/distributed_monitoring/proxy_set.png















   
