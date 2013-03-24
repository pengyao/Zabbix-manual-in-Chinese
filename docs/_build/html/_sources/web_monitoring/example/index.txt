=====================================
2 方案真实场景
=====================================

.. contents::

概述
-----------------------

本小节将一步步地实现一个web监控的真实例子.

使用Zabbix Web对Zabbix web接口进行监控，我们想监控它是否可用，是否提供正确的内容，响应速度等. 要完成本监控，需要知道Zabbix web接口的帐户名和密码.

方案
---------------------

**第一步**

添加一个新的主机应用(application).

前往 `Configuration` -> `Host` ,选择你想进行web监控的主机，点击`Applications`,在application页面点击 `Create application` .

.. image:: /_static/images/web_monitoring/new_application.png

如果你已经有了一个合适的应用(application)，本步并不是必须的. 你也需要知道如果主机(host)不存在，如何去创建它.

**第二步**

添加一个新的web方案

我们将添加一个为了监控Zabbix web接口的方案. 本方案将执行若干步骤(step).

前往 `Configuration` -> `Web` ，在下拉框中选择主机，然后点击 `Create scenario`.

.. image:: /_static/images/web_monitoring/new_scenario.png

在这个新的方案表单中，点击 `Select` 选择我们刚刚添加的application.

注意我们也需要创建两个宏，分别为{user}和{password}.

**第三步**

定义本方案的各个步骤(step).

点击 `Add` 按钮选择添加步骤的 `Steps` 标签页.

`Web方案第一步`

我们首先创建检查首页回应的步骤，返回的状态码为 200,内容中包含"SIA Zabbix"字样.

.. image:: /_static/images/web_monitoring/scenario_step1.png

配置完成后，点击 `Add` 

`Web方案第二步`

我们需要登录到Zabbix前端，这就需要之前我们添加过两个宏,{user}和{password}

.. image:: /_static/images/web_monitoring/scenario_step2.png

.. warning::
    
   Zabbix前端登录时使用JavaScript跳转,因此我们必须先完成登录，才能在后续步骤中完成登录后的检查. 同时登录步骤必须使用完整的URL到 *index.php* 页面.
	  
所有的post变量必须在同一行,并且用 *&* 符号进行连接. 例如登录Zabbix前端的字符串为::
   
   name=Admin&password=zabbix&enter=Sign in

如果在本例中使用宏，字符串将变成::

   name={user}&password={password}&enter=Sign in

`Web方案第三步`

登录后，我们应该验证是否登录成功，因此我们在登录后的检查页面中含有的字符串，例如 *Profile* 链接在右上角

.. image:: /_static/images/web_monitoring/scenario_step3.png


`Web方案第四步`

当前我们已经验证前端可以访问，并且我们已经进行了登录，并检查了登录后的内容，现在我们应该退出登录，除非Zabbix数据库中大量的已打开的session记录被清除.

.. image:: /_static/images/web_monitoring/scenario_step4.png


`完整步骤的配置`

完成的步骤配置如下:

.. image:: /_static/images/web_monitoring/scenario_steps.png


**第四步**

保存已完成的web监控方案.

·Monitoring· -> `Web` 下对应应用的方案如下:

.. image:: /_static/images/web_monitoring/web_checks.png

点击方案名，可以查看更详细的统计:

.. image:: /_static/images/web_monitoring/scenario_details.png





   
