.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.
   
=====================
Monitoring the System
=====================

The **Monitor** icon on the Contrail Controller provides numerous options so you can view and analyze usage and other activity associated with all nodes of the system, through the use of reports, charts, and detailed lists of configurations and system activities.

Monitor pages support monitoring of infrastructure components—control nodes, virtual routers, analytics nodes, and config nodes. Additionally, users can monitor networking and debug components.

Use the menu options available from the **Monitor** icon to configure and view the statistics you need for better understanding of the activities in your system. See `Figure 123`_ 

.. _Figure 123: 

*Figure 123* : Monitor Menu

.. figure:: s041506.gif

See `Table 41`_ for descriptions of the items available under each of the menu options from the **Monitor** icon.

.. _Table 41: 


*Table 41* : Monitor Menu Options

	+-------------------+------------------------------------------------------------------------------------------------------+
	| Option            | Description                                                                                          |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Infrastructure    | Shows “at-a-glance” status view of the infrastructure components, including the numbers of virtual   |
	| > Dashboard       | routers, control nodes, analytics nodes, and config nodes currently operational, and a bubble chart  |
	|                   | of virtual routers showing the CPU and memory utilization, log messages, system information, and     |
	|                   | alerts. See `Monitor > Infrastructure > Dashboard`_.                                                 |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Infrastructure    | View a summary for all control nodes in the system, and for each control node, view:                 |
	| > Control Nodes   |  -  Graphical reports of memory usage and average CPU load.                                          |
	|                   |  -  Console information for a specified time period.                                                 |
	|                   |  -  A list of all peers with details about type, ASN, and the like.                                  |
	|                   |  -  A list of all routes, including next hop, source, local preference, and the like.                |
	|                   | See `Monitor > Infrastructure > Control Nodes`_.                                                     |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Infrastructure    | View a summary of all vRouters in the system, and for each vRouter, view:                            |
	| > Virtual Routers |  -  Graphical reports of memory usage and average CPU load.                                          |
	|                   |  -  Console information for a specified time period.                                                 |
	|                   |  -  A list of all interfaces with details such as label, status, associated network, IP address, and |
	|                   |     the like.                                                                                        |
	|                   |  -  A list of all associated networks with their ACLs and VRFs.                                      |
	|                   |  -  A list of all active flows with source and destination details, size, and time.                  |
	|                   | See `Monitor > Infrastructure > Virtual Routers`_.                                                   |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Infrastructure    | View activity for the analytics nodes, including memory and CPU usage, analytics host names,         |
	| > Analytics Nodes | IP address, status, and more. See `Monitor > Infrastructure > Analytics Nodes`_.                     |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Infrastructure    | View activity for the config nodes, including memory and CPU usage, config host names, IP address,   |
	| > Config Nodes    | status, and more. See `Monitor > Infrastructure > Config Nodes`_.                                    |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Networking        | For all virtual networks for all projects in the system, view graphical traffic statistics,including:|
	| > Networks        |  -  Total traffic in and out.                                                                        |
	|                   |  -  Inter VN traffic in and out.                                                                     |
	|                   |  -  The most active ports, peers, and flows for a specified duration.                                |
	|                   |  -  All traffic ingress and egress from connected networks, including their attached policies.       |
	|                   | See `Monitor > Networking`_.                                                                         |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Networking        | For all virtual networks for all projects in the system, view graphical traffic statistics,including:|
	| > Dashboard       |  -  Total traffic in and out.                                                                        |
	|                   |  -  Inter VN traffic in and out.                                                                     |
	|                   | You can view the statistics in varying levels of granularity, for example, for a whole project,      |
	|                   | or for a single network. See `Monitor > Networking`_.                                                |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Networking        | View essential information about projects in the system including name, associated networks,         |
	| > Projects        | and traffic in and out.                                                                              |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Networking        | View essential information about networks in the system including name and traffic in and out.       |
	| > Netwroks        |                                                                                                      |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Networking        | View essential information about instances in the system including name, associated networks,        |
	| > Instances       | interfaces, vRouters, and traffic in and out.                                                        |
	+-------------------+------------------------------------------------------------------------------------------------------+
	| Debug             | - Add and manage packet analyzers.                                                                   |
	| > Packet          | - Attach packet captures and configure their details.                                                |
	| Capture           | - View a list of all packet analyzers in the system and the details of their configurations,         |
	|                   |    including source and destination networks, ports, and IP addresses.                               |
	+-------------------+------------------------------------------------------------------------------------------------------+

**Related Documentation**

-  `Monitor > Infrastructure > Dashboard`_ 

-  `Monitor > Infrastructure > Control Nodes`_ 

-  `Monitor > Infrastructure > Virtual Routers`_ 

-  `Monitor > Networking`_ 

-  `Query > Logs`_ 

-  `Query > Flows`_ 

.. _Monitor > Infrastructure > Dashboard: monitor-dashboard-vnc.html

.. _Monitor > Infrastructure > Control Nodes: monitoring-infrastructure-vnc.html

.. _Monitor > Infrastructure > Virtual Routers: monitoring-vrouters-vnc.html

.. _Monitor > Infrastructure > Analytics Nodes: monitor-analytics-vnc.html

.. _Monitor > Infrastructure > Config Nodes: monitor-config-vnc.html

.. _Monitor > Networking: monitoring-networking-vnc.html

.. _Monitor > Networking: monitoring-networking-vnc.html

.. _Monitor > Infrastructure > Dashboard: monitor-dashboard-vnc.html

.. _Monitor > Infrastructure > Control Nodes: monitoring-infrastructure-vnc.html

.. _Monitor > Infrastructure > Virtual Routers: monitoring-vrouters-vnc.html

.. _Monitor > Networking: monitoring-networking-vnc.html

.. _Query > Logs: monitoring-syslog-vnc.html

.. _Query > Flows: monitoring-flow-vnc.html
