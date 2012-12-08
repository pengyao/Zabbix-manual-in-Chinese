=============================
5  Java gateway
=============================

.. contents::


概述
---------------------------

Zabbix 2.0通过被称为"Zabbix Java gateway"的新增Zabbix守护进程提供了原生对JMX应用的监控. Zabbix Java gateway是采用Java编写的一个守护进程.当Zabbix server想知道主机JMX计数器的值时，
它请求Zabbix Java gateway，Zabbix Java gateway将利用 `JMX管理API <http://java.sun.com/javase/technologies/core/mntr-mgmt/javamanagement/>`_  去请求远程的有关应用.应用不需要额外安装软件，只需要在启动时在命令行指定 *-Dcom.sun.management.jmxremote* 选项.

Java gateway接受来自Zabbix server或者proxy的连接，只能使用"被动代理"的方式. As opposed to Zabbix proxy, it may also be used from Zabbix proxy (Zabbix proxies cannot be chained).
在Zabbix server或代理的配置文件中指定访问JAVA gateway.因此在每一个Zabbix server或代理中只能配置一个Java gateway.如果一个主机有 **JMX agent** 及其他类型的监控项,则只有 **JMX agent** 类型的监控项可以通过Java gateway进行监控.

当在Java gateway上的一个监控项值更新了,Zabbix server或代理将连接Java gateway请求该值, which Java gateway in turn retrieves and passes back to the server or proxy. 同样的，Java gateway不会缓存任何值.

Zabbix server或代理可以通过 **StartJavaPollers** 控制连接Java gateway的进程. Java gateway在内部通过 **START_POLLERS** 控制选项使用多线程启动. 在服务端，如果一个连接请求超过了 **Timeout** 设定的秒数，连接将会终止,但Java gateway也许此时依然忙于从JMX计数器中检索该值.

Zabbix server or proxy will try to pool requests to a single JMX target together as much as possible (affected by item intervals) and send them to the Java Gateway in a single connection for better performance.

建议 **StartJavaPollers** 小于或等于 **START_POLLERS** ，否则可能导致当连接Java gateway时而Java gateway没有多余的线程进行处理.

以下内容将详细讲讲如何安装和运行Zabbix Java gateway，如何配置Zabbix server(或代理)利用Zabbix Java gateway完成JMX监控，如何在Zabbix GUI配置JMX计数器监控项.

Getting Java gateway
----------------------

有两种方式得到Java gateway,一种是通过Zabbix网站下载Java gateway包，另一种是通过源码编译Java gateway.

通过Zabbix网站下载
^^^^^^^^^^^^^^^^^^^^^

该方法当前是无效的，不过未来你可以在Zabbix网站上下载Java gateway压缩包 (译者注：这算是寅吃卯粮不，哈哈)

通过源码编译
^^^^^^^^^^^^^^^^^^^^^

为了编译Java gateway，你需要在运行./configure时指定--enable-java选项. 建议在安装时指定--prefix选项而并非使用默认的/usr/local, 因为在安装Java gateway时将创建整个目录树，而并非单一的可执行文件.::

   $ ./configure --enable-java --prefix=$PREFIX
   
使用make完成Java gateway编译并打包成一个JAR文件. 注意本步将使用javac和jar,因此你需要保证它们在path中.::
  
   $ make

现在你将在src/zabbix_java/bin下得到zabbix-java-gateway-$VERSION.jar文件. 如果你想在指定的目录下轻松的使用Java gateway以完成配置和运行，请确保有足够的权限运行 make install. ::

   $ make install

   
Java gateway 文件预览
------------------------------------

不管你怎么得到Java gateway, 最终在$PREFIX/sbin/zabbix_java下你会看到shell脚本、JAR包和配置. 文件的用途如下:

::

   bin/zabbix-java-gateway-$VERSION.jar
 
Java gateway JAR文件

::
   
   lib/logback-core-0.9.27.jar
   lib/logback-classic-0.9.27.jar
   lib/slf4j-api-1.6.1.jar
   lib/org-json-2012-12-28.jar
   
Java gateway依赖 `Logback <http://logback.qos.ch/>`_ `SLF4J <http://www.slf4j.org/>`_ `JSON.org <http://www.json.org/>`_ 库

::

   lib/logback.xml
   lib/logback-console.xml
   
Logback的配置文件

::

   shutdown.sh
   startup.sh
   
方便不进行启动/关闭Java gateway的脚本.

::
   
   setting.sh
   
Configuration file that is sourced by startup and shutdown scripts above.


配置和运行Java gateway
----------------------------------

默认情况下，Java gateway监听10052端口. 如果你计划使用不同的端口来运行Java gateway，你需要通过setting.sh脚本指定下需要的端口.
请访问 `Java gateway配置文件` 获得如何指定该选项以及其他选项.

   .. warning::
   
      10052端口并没有在 `IANA <http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.txt>`_ 注册过

	  
一旦你完成了配置，你可以通过startup脚本来启动Java gateway::

   $ ./startup.sh

如果你不需要Java gateway，你可以运行shutdown脚本关闭它::

   $ ./shutdown.sh

不像server和代理(proxy)，Java gateway是轻量级的，并不需要数据库支持.


配置server使用Java gateway
------------------------------------------

当前Java gateway已经运行，接下来你需要告诉Zabbix server如何找到Zabbix Java gateway. 因此你需要在 `server配置文件` 中指定JavaGateway及JavaGateway端口.
如果JMX应用采用Zabbix代理进行监控的话，你需要在 `代理配置文件` 中指定对应的连接参数.

::

   JavaGateway=192.168.3.14
   JavaGatewayPort=10052

默认情况下，server并不会派生出任何进程去进行JMX监控。如果你想使用完成JMX监控，你需要指定预派生出来的Java pollers进程数，你也可过同类的方式指定常见的pollers和trappers.

::

   StartJavaPollers=5

在完成配置后，千万不要忘记要重启server(或代理)


Debugging Java gateway
----------------------------

万一Java gateway出现了若干问题，在前段可以看到的监控项报错信息并不充分，你也可以通过查看Java gateway日志文件获得更多信息.

默认情况下，Java gateway将记录日志到/tmp/zabbix_java.log文件中，log级别为"info". 有时你觉得"info"级别得到的信息并不够，你需要修改级别为"debug".
你可以通过修改lib/logback.xml将<root>标签更改为"debug"以获取日志级别的增加.

::

   <root level="debug">
      <appender-ref ref="FILE" />
   </root>	

需要主机的是，并不像Zabbix server或proxy那样，修改完logback.xml并不需要重启Zabbix Java gateway. 修改后的配置将会自动被加载. 当你完成了debugging,你可以将log级别替换为"info".

如果你想将日志记录到其他文件或者其他方式完成存储（如数据库），按照你的需求调整logback.xml文件即可。 欲了解更多请访问 `Logback手册 <http://logback.qos.ch/manual/>`_

有时为了方便进行debug,你也许不想采用daemon方式而想采用控制台的方式. 你需要注释掉setting.sh脚本中 **PID_FILE**  变量。一旦没有找到 **PID_FILE** 参数，startup.sh脚本将直接以控制台方式运行.
Logback也将使用lib/logback-console.xml文件. 不仅仅只是记录到控制台，记录级别也将变更为"debug".

Finally, note that since Java gateway uses SLF4J for logging, you can replace Logback with the framework of your choice by placing an appropriate JAR file in lib directory. 访问 `SLF4J手册 <http://www.slf4j.org/manual.html>`_ 获得更多.



   

