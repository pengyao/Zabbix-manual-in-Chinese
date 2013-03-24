=================
主机
=================

* 贡献者： Nexpro (https://github.com/nexpro) 

Hosts are exported with many related objects and object relations.

主机导出包含:
    * 主机数据
    * 主机间隔数据
    * 组关系
    * 模板关系
    * 接口
    * 宏
    * 应用
    * 项目
    * 所有原型的发现规则    

当主机导入或者更新是,它只能链接到附加的模板同时不能从任何地方取消关联

::

    <hosts>
        <host>
            <host>Zabbix server</host>
            <name>Zabbix server</name>
            <proxy/>
            <status>0</status>
            <ipmi_authtype>-1</ipmi_authtype>
            <ipmi_privilege>2</ipmi_privilege>
            <ipmi_username/>
            <ipmi_password/>
            <templates/>
            <groups>
                <group>
                    <name>Zabbix servers</name>
                </group>
            </groups>
            <interfaces>
                <interface>
                    <default>1</default>
                    <type>1</type>
                    <useip>1</useip>
                    <ip>127.0.0.1</ip>
                    <dns/>
                    <port>20001</port>
                    <interface_ref>if1</interface_ref>
                </interface>
            </interfaces>
            <applications>
                <application>
                    <name>Memory</name>
                </application>
                <application>
                    <name>Zabbix agent</name>
                </application>
            </applications>
            <items>
                <item>
                    <name>Agent ping</name>
                    <type>0</type>
                    <snmp_community/>
                    <multiplier>0</multiplier>
                    <snmp_oid/>
                    <key>agent.ping</key>
                    <delay>60</delay>
                    <history>7</history>
                    <trends>365</trends>
                    <status>0</status>
                    <value_type>3</value_type>
                    <allowed_hosts/>
                    <units/>
                    <delta>0</delta>
                    <snmpv3_securityname/>
                    <snmpv3_securitylevel>0</snmpv3_securitylevel>
                    <snmpv3_authpassphrase/>
                    <snmpv3_privpassphrase/>
                    <formula>1</formula>
                    <delay_flex/>
                    <params/>
                    <ipmi_sensor/>
                    <data_type>0</data_type>
                    <authtype>0</authtype>
                    <username/>
                    <password/>
                    <publickey/>
                    <privatekey/>
                    <port/>
                    <description>The agent always returns 1 for this item. It could be used in combination with 
					nodata() for availability check.</description>
                    <inventory_link>0</inventory_link>
                    <applications>
                        <application>
                            <name>Zabbix agent</name>
                        </application>
                    </applications>
                    <valuemap>
                        <name>Zabbix agent ping status</name>
                    </valuemap>
                    <interface_ref>if1</interface_ref>
                </item>
                <item>
                    <name>Available memory</name>
                    <type>0</type>
                    <snmp_community/>
                    <multiplier>0</multiplier>
                    <snmp_oid/>
                    <key>vm.memory.size[available]</key>
                    <delay>60</delay>
                    <history>7</history>
                    <trends>365</trends>
                    <status>0</status>
                    <value_type>3</value_type>
                    <allowed_hosts/>
                    <units>B</units>
                    <delta>0</delta>
                    <snmpv3_securityname/>
                    <snmpv3_securitylevel>0</snmpv3_securitylevel>
                    <snmpv3_authpassphrase/>
                    <snmpv3_privpassphrase/>
                    <formula>1</formula>
                    <delay_flex/>
                    <params/>
                    <ipmi_sensor/>
                    <data_type>0</data_type>
                    <authtype>0</authtype>
                    <username/>
                    <password/>
                    <publickey/>
                    <privatekey/>
                    <port/>
                    <description>Available memory is defined as free+cached+buffers memory.</description>
                    <inventory_link>0</inventory_link>
                    <applications>
                        <application>
                            <name>Memory</name>
                        </application>
                    </applications>
                    <valuemap/>
                    <interface_ref>if1</interface_ref>
                </item>
            </items>
            <discovery_rules>
                <discovery_rule>
                    <name>Mounted filesystem discovery</name>
                    <type>0</type>
                    <snmp_community/>
                    <snmp_oid/>
                    <key>vfs.fs.discovery</key>
                    <delay>3600</delay>
                    <status>0</status>
                    <allowed_hosts/>
                    <snmpv3_securityname/>
                    <snmpv3_securitylevel>0</snmpv3_securitylevel>
                    <snmpv3_authpassphrase/>
                    <snmpv3_privpassphrase/>
                    <delay_flex/>
                    <params/>
                    <ipmi_sensor/>
                    <authtype>0</authtype>
                    <username/>
                    <password/>
                    <publickey/>
                    <privatekey/>
                    <port/>
                    <filter>{#FSTYPE}:@File systems for discovery</filter>
                    <lifetime>30</lifetime>
                    <description>Discovery of file systems of different types as defined in global regular 
					expression &quot;File systems for discovery&quot;.</description>
                    <item_prototypes>
                        <item_prototype>
                            <name>Free disk space on $1</name>
                            <type>0</type>
                            <snmp_community/>
                            <multiplier>0</multiplier>
                            <snmp_oid/>
                            <key>vfs.fs.size[{#FSNAME},free]</key>
                            <delay>60</delay>
                            <history>7</history>
                            <trends>365</trends>
                            <status>0</status>
                            <value_type>3</value_type>
                            <allowed_hosts/>
                            <units>B</units>
                            <delta>0</delta>
                            <snmpv3_securityname/>
                            <snmpv3_securitylevel>0</snmpv3_securitylevel>
                            <snmpv3_authpassphrase/>
                            <snmpv3_privpassphrase/>
                            <formula>1</formula>
                            <delay_flex/>
                            <params/>
                            <ipmi_sensor/>
                            <data_type>0</data_type>
                            <authtype>0</authtype>
                            <username/>
                            <password/>
                            <publickey/>
                            <privatekey/>
                            <port/>
                            <description/>
                            <inventory_link>0</inventory_link>
                            <applications>
                                <application>
                                    <name>Filesystems</name>
                                </application>
                            </applications>
                            <valuemap/>
                            <interface_ref>if1</interface_ref>
                        </item_prototype>
                    </item_prototypes>
                    <trigger_prototypes>
                        <trigger_prototype>
                            <expression>{Zabbix server 2:vfs.fs.size[{#FSNAME},pfree].last(0)}&lt;20</expression>
                            <name>Free disk space is less than 20% on volume {#FSNAME}</name>
                            <url/>
                            <status>0</status>
                            <priority>2</priority>
                            <description/>
                            <type>0</type>
                        </trigger_prototype>
                    </trigger_prototypes>
                    <graph_prototypes>
                        <graph_prototype>
                            <name>Disk space usage {#FSNAME}</name>
                            <width>600</width>
                            <height>340</height>
                            <yaxismin>0.0000</yaxismin>
                            <yaxismax>0.0000</yaxismax>
                            <show_work_period>0</show_work_period>
                            <show_triggers>0</show_triggers>
                            <type>2</type>
                            <show_legend>1</show_legend>
                            <show_3d>1</show_3d>
                            <percent_left>0.0000</percent_left>
                            <percent_right>0.0000</percent_right>
                            <ymin_type_1>0</ymin_type_1>
                            <ymax_type_1>0</ymax_type_1>
                            <ymin_item_1>0</ymin_item_1>
                            <ymax_item_1>0</ymax_item_1>
                            <graph_items>
                                <graph_item>
                                    <sortorder>0</sortorder>
                                    <drawtype>0</drawtype>
                                    <color>C80000</color>
                                    <yaxisside>0</yaxisside>
                                    <calc_fnc>2</calc_fnc>
                                    <type>2</type>
                                    <item>
                                        <host>Zabbix server 2</host>
                                        <key>vfs.fs.size[{#FSNAME},total]</key>
                                    </item>
                                </graph_item>
                                <graph_item>
                                    <sortorder>1</sortorder>
                                    <drawtype>0</drawtype>
                                    <color>00C800</color>
                                    <yaxisside>0</yaxisside>
                                    <calc_fnc>2</calc_fnc>
                                    <type>0</type>
                                    <item>
                                        <host>Zabbix server 2</host>
                                        <key>vfs.fs.size[{#FSNAME},free]</key>
                                    </item>
                                </graph_item>
                            </graph_items>
                        </graph_prototype>
                    </graph_prototypes>
                    <interface_ref>if1</interface_ref>
                </discovery_rule>
            </discovery_rules>
            <macros>
                <macro>
                    <macro>{$M1}</macro>
                    <value>m1</value>
                </macro>
                <macro>
                    <macro>{$M2}</macro>
                    <value>m2</value>
                </macro>
            </macros>
            <inventory/>
        </host>
    </hosts>

hosts/host
-------------

    +----------------+------------+---------------+------------+
    |参数            |     类型   |   描述        |   详细信息 |
    +================+============+===============+============+
    |host            |     字符串 |   主机名      |            |
    +----------------+------------+---------------+------------+
    |name            |     字符串 |   可见的主机名|            |
    +----------------+------------+---------------+------------+
    |status          |     整数   |   主机状态    |            |
    +----------------+------------+---------------+------------+
    |proxy           |     整数   |   代理名称    |            |
    +----------------+------------+---------------+------------+
    |ipmi_authtype   |     整数   |   IPMI认证类型|            |
    +----------------+------------+---------------+------------+
    |ipmi_privilege  |     整数   |   IPMI权限    |            |
    +----------------+------------+---------------+------------+
    |ipmi_username   |     字符串 |   IPMI用户名  |            |
    +----------------+------------+---------------+------------+
    |ipmi_password   |     字符串 |   IPMI密码    |            |
    +----------------+------------+---------------+------------+

hosts/host/groups/group
---------------------------

    +-------------+----------+------------+-----------------------------+
    | 参数        |   类型   |   描述     |       详细信息              |
    +=============+==========+============+=============================+
    | name        |   字符串 |   组名     |                             |
    +------------------------+------------+-----------------------------+


hosts/host/templates/template
--------------------------------

    +------------------------+------------+-----------------------------+
    | 参数                   |  类型      | 描述                        |
    +========================+============+=============================+
    | name                   |  整数      |  接口状态                   |
    +                        |            +-----------------------------+
    |                        |            +  0 - 不是默认接口           |
    +                        |            +-----------------------------+
    |                        |            +  1 - 默认接口               |
    +------------------------+------------+-----------------------------+
    | type                   | 整数       +  接口类型                   |
    +------------------------+------------+-----------------------------+
    |                                     |  1 - agent                  |
    +                                     +-----------------------------+
    |                                     |  2 - SNMP                   |
    +                                     +-----------------------------+
    |                                     |  3 - IPMI                   |
    +                                     +-----------------------------+
    |                                     |  4 - JMX                    |
    +------------------------+------------+-----------------------------+
    | useip                  | 整数       | 如何连接到主机              |
    +------------------------+------------+-----------------------------+
    |                                     |  0 - 使用DNS名称            |
    +                                     +-----------------------------+
    |                                     |  1 - 使用IP地址             |
    +------------------------+------------+-----------------------------+
    | ip                     | 字符串     | ip地址,可以是ipv4或者ipv6   |         
    +------------------------+------------+-----------------------------+
    | dns                    | 字符串     | DNS名称                     |
    +------------------------+------------+-----------------------------+
    | port                   | 字符串     | 端口号                      |
    +------------------------+------------+-----------------------------+
    | interface_ref          | 字符串     | 在项目中使用的接口引用名称  |
    +------------------------+------------+-----------------------------+



hosts/host/interfaces/interface
---------------------------------

    +------------------------+------------+-----------+------------------+
    |参数                    | 类型       | 描述      |       详细信息   |
    +========================+============+===========+==================+
    |default                 | 整数       | 主机名    |                  |
    +------------------------+------------+-----------+------------------+


hosts/host/items/item
------------------------------

    +------------------------+------------+-------------------------------------+
    | 参数                   |      类型  |    描述                             | 
    +========================+============+=====================================+
    |                        |            | Item type:                          | 
    |                        |            +-------------------------------------+
    |                        |            |  0 - Zabbix agent                   |
    |                        |            +-------------------------------------+
    |                        |            |  1 - SNMPv1                         |
    |                        |            +-------------------------------------+
    |                        |            |  2 - Trapper                        |
    |                        |            +-------------------------------------+
    |                        |            |  3 - Simple check                   |
    |                        |            +-------------------------------------+
    |                        |            |  4 - SNMPv2                         |
    |                        |            +-------------------------------------+
    |                        |            |  5 - Internal                       |
    |                        |            +-------------------------------------+
    |                        |            |  6 - SNMPv3                         |
    |                        |            +-------------------------------------+
    |                        |            |  7 - Active check                   |
    |                        |            +-------------------------------------+
    |    type                |  整数      |  8 - Aggregate                      |
    |                        |            +-------------------------------------+
    |                        |            |  9 - HTTP test (Web监控方案步骤)    |
    |                        |            +-------------------------------------+
    |                        |            |  10 - External                      |
    |                        |            +-------------------------------------+
    |                        |            |  11 - Database monitor              |
    |                        |            +-------------------------------------+
    |                        |            |  12 - IPMI                          |
    |                        |            +-------------------------------------+
    |                        |            |   13 - SSH                          |
    |                        |            +-------------------------------------+
    |                        |            |  14 - telnet                        |
    |                        |            +-------------------------------------+
    |                        |            |  15 - Calculated                    |
    |                        |            +-------------------------------------+
    |                        |            |  16 - JMX                           |
    |                        |            +-------------------------------------+
    |                        |            |  17 - SNMP trap                     |
    +------------------------+------------+-------------------------------------+
    | snmp_community         |     字符串 |    SNMP 团体名                      |
    +------------------------+------------+-------------------------------------+
    | snmp_oid               |     字符串 |    SNMP OID                         |
    +------------------------+------------+-------------------------------------+
    | port                   |     整数   |    项目定制端口                     |
    +------------------------+------------+-------------------------------------+
    | name                   |     字符串 |    项目名称                         |
    +------------------------+------------+-------------------------------------+
    | key                    |     字符串 |    项目关键字                       |
    +------------------------+------------+-------------------------------------+
    | delay                  |     整数   |    检查间隔                         |
    +------------------------+------------+-------------------------------------+
    | history                |      整数  |    历史数据保留天数(单位天)         |
    +------------------------+------------+-------------------------------------+
    | trends                 |      整数  |    趋势数据保留天数(单位天)         |
    +------------------------+------------+-------------------------------------+
    | status                 |      整数  |    项目状态                         |
    +------------------------+------------+-------------------------------------+
    | value_type             |      整数  |    值类型                           |
    +------------------------+------------+-------------------------------------+
    | trapper_hosts          |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | units                  |     字符串 |    值单位                           |
    +------------------------+------------+-------------------------------------+
    | multiplier             |     整数   |    值的乘数                         |
    +------------------------+------------+-------------------------------------+
    | delta                  |     整数   |    Store values as delta            |
    +------------------------+------------+-------------------------------------+
    | snmpv3_securityname    |     字符串 |    SNMPv3 安全名称                  |
    +------------------------+------------+-------------------------------------+
    | snmpv3_securitylevel   |     整数   |    SNMPv3 安全级别                  |
    +------------------------+------------+-------------------------------------+
    | snmpv3_authpassphrase  |     字符串 |    SNMPv3 认证口令                  |
    +------------------------+------------+-------------------------------------+
    | snmpv3_privpassphrase  |     字符串 |    SNMPv3 私有口令                  |
    +------------------------+------------+-------------------------------------+
    | formula                |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | delay_flex             |     字符串 |    弹性延迟                         |
    +------------------------+------------+-------------------------------------+
    | params                 |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | ipmi_sensor            |     字符串 |    IPMI 传感器                      |
    +------------------------+------------+-------------------------------------+
    | data_type              |     整数   |                                     |
    +------------------------+------------+-------------------------------------+
    | authtype               |     整数   |                                     |
    +------------------------+------------+-------------------------------------+
    | username               |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | password               |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | publickey              |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | privatekey             |     字符串 |                                     |
    +------------------------+------------+-------------------------------------+
    | interface_ref          |     字符串 |    主机接口引用                     |
    +------------------------+------------+-------------------------------------+
    | description            |     字符串 |    项目描述                         |
    +------------------------+------------+-------------------------------------+
    | inventory_link         |     整数   |   主机间隔字段号,将更新项目返回的值 |   
    +------------------------+------------+-------------------------------------+
    | applications           |            |    项目应用                         |
    +------------------------+------------+-------------------------------------+

hosts/host/items/item/applications/application
----------------------------------------------------

    +------------------------+------------+-----------+------------------+
    |    参数                | 类型       |  描述     |         详细信息 |
    +========================+============+===========+==================+
    |    name                | 字符串     |  应用名称 |                  |
    +------------------------+------------+-----------+------------------+

