.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

====================
Monitor > Networking
====================

The **Monitor -> Networking** pages give an overview of the networking traffic statistics and health of domains, projects within domains, virtual networks within projects, and virtual machines within virtual networks.

-  `Monitor > Networking Menu Options`_ 


-  `Monitor -> Networking -> Dashboard`_ 


-  `Monitor > Networking > Projects`_ 


-  `Monitor Projects Detail`_ 


-  `Monitor > Networking > Networks`_ 



Monitor > Networking Menu Options
=================================

`Figure 98`_ shows the menu options available under **Monitor > Networking** .

.. _Figure 98: 

*Figure 98* : Monitor Networking Menu Options

.. figure:: 64512.gif


Monitor -> Networking -> Dashboard
==================================

Select **Monitor -> Networking -> Dashboard** to gain insight into usage statistics for domains, virtual networks, projects, and virtual machines. When you select this option, the Traffic Statistics for Domain window is displayed as shown in `Figure 99`_ .

.. _Figure 99: 

*Figure 99* : Traffic Statistics for Domain Window

.. figure:: s041588.gif

`Table 41`_ describes the fields in the Traffic Statistics for Domain window.

.. _Table 41: 


*Table 41* : Projects Summary Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Total Traffic In**              | The volume of traffic into this   |
|                                   | domain                            |
+-----------------------------------+-----------------------------------+
| **Total Traffic Out**             | The volume of traffic out of this |
|                                   | domain.                           |
+-----------------------------------+-----------------------------------+
| **Inter VN Traffic In**           | The volume of inter-virtual       |
|                                   | network traffic into this domain. |
+-----------------------------------+-----------------------------------+
| **Inter VN Traffic Out**          | The volume of inter-virtual       |
|                                   | network traffic out of this       |
|                                   | domain.                           |
+-----------------------------------+-----------------------------------+
| **Projects**                      | This chart displays the networks  |
|                                   | and interfaces for projects with  |
|                                   | the most throughput over the past |
|                                   | 30 minutes. Click **Projects**    |
|                                   | then select **Monitor >           |
|                                   | Networking > Projects**, to       |
|                                   | display more detailed statistics. |
+-----------------------------------+-----------------------------------+
| **Networks**                      | This chart displays the networks  |
|                                   | for projects with the most        |
|                                   | throughput over the past 30       |
|                                   | minutes. Click **Networks** then  |
|                                   | select **Monitor > Networking >   |
|                                   | Networks**, to display more       |
|                                   | detailed statistics.              |
+-----------------------------------+-----------------------------------+


Monitor > Networking > Projects
===============================

Select **Monitor > Networking > Projects** to see information about projects in the system. See `Figure 100`_ .

.. _Figure 100: 

*Figure 100* : Monitor > Networking > Projects

.. figure:: s041589.gif

See `Table 42`_ for descriptions of the fields on this screen.

.. _Table 42: 


*Table 42* : Projects Summary Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Projects**                      | The name of the project. You can  |
|                                   | click the name to access details  |
|                                   | about connectivity for this       |
|                                   | project.                          |
+-----------------------------------+-----------------------------------+
| **Networks**                      | The volume of inter-virtual       |
|                                   | network traffic out of this       |
|                                   | domain.                           |
+-----------------------------------+-----------------------------------+
| **Traffic In**                    | The volume of traffic into this   |
|                                   | domain.                           |
+-----------------------------------+-----------------------------------+
| **Traffic Out**                   | The volume of traffic out of this |
|                                   | domain.                           |
+-----------------------------------+-----------------------------------+


Monitor Projects Detail
=======================

You can click any of the projects listed on the Projects Summary to get details about connectivity, source and destination port distribution, and instances. When you click an individual project, the Summary tab for Connectivity Details is displayed as shown in `Figure 101`_ . Hover over any of the connections to get more details.

.. _Figure 101: 

*Figure 101* : Monitor Projects Connectivity Details

.. figure:: s041846.gif

In the Connectivity Details window you can click the links between the virtual networks to view the traffic statistics between the virtual networks.

The Traffic Statistics information is also available when you select **Monitor > Networking > Networks** as shown in `Figure 102`_ .

.. _Figure 102: 

*Figure 102* : Traffic Statistics Between Networks

.. figure:: s041590.gif

In the Connectivity Details window you can click the Instances tab to get a summary of details for each of the instances in this project.

.. _Figure 103: 

*Figure 103* : Projects Instances Summary

.. figure:: s041593.gif

See Table 3 for a description of the fields on this screen.

.. _Table 43: 


*Table 43* : Projects Instances Summary Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Instance**                      | The name of the instance. Click   |
|                                   | the name then select **Monitor >  |
|                                   | Networking > Instances** to       |
|                                   | display details about the traffic |
|                                   | statistics for this instance.     |
+-----------------------------------+-----------------------------------+
| **Virtual Network**               | The virtual network associated    |
|                                   | with this instance.               |
+-----------------------------------+-----------------------------------+
| **Interfaces**                    | The number of interfaces          |
|                                   | associated with this instance.    |
+-----------------------------------+-----------------------------------+
| **vRouter**                       | The name of the vRouter           |
|                                   | associated with this instance.    |
+-----------------------------------+-----------------------------------+
| **IP Address**                    | Any IP addresses associated with  |
|                                   | this instance.                    |
+-----------------------------------+-----------------------------------+
| **Floating IP**                   | Any floating IP addresses         |
|                                   | associated with this instance.    |
+-----------------------------------+-----------------------------------+
| **Traffic (In/Out)**              | The volume of traffic in KB or MB |
|                                   | that is passing in and out of     |
|                                   | this instance.                    |
+-----------------------------------+-----------------------------------+

Select **Monitor > Networking > Instances** to display instance traffic statistics as shown in `Figure 104`_ .

.. _Figure 104: 

*Figure 104* : Instance Traffic Statistics

.. figure:: s041595.gif


Monitor > Networking > Networks
===============================

Select **Monitor > Networking > Networks** to view a summary of the virtual networks in your system. See `Figure 105`_ .

.. _Figure 105: 

*Figure 105* : Network Summary

.. figure:: s041873.gif

.. _Table 44: 


*Table 44* : Network Summary Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Network**                       | The domain and network name of    |
|                                   | the virtual network. Click the    |
|                                   | arrow next to the name to display |
|                                   | more information about the        |
|                                   | network, including the number of  |
|                                   | ingress and egress flows, the     |
|                                   | number of ACL rules, the number   |
|                                   | of interfaces, and the total      |
|                                   | traffic in and out.               |
+-----------------------------------+-----------------------------------+
| **Instances**                     | The number of instances launched  |
|                                   | in this network.                  |
+-----------------------------------+-----------------------------------+
| **Traffic (In/Out)**              | The volume of inter-virtual       |
|                                   | network traffic in and out of     |
|                                   | this network.                     |
+-----------------------------------+-----------------------------------+
| **Throughput (In/Out)**           | The throughput of inter-virtual   |
|                                   | network traffic in and out of     |
|                                   | this network.                     |
+-----------------------------------+-----------------------------------+

At **Monitor > Networking > Networks** you can click on the name of any of the listed networks to get details about the network connectivity, traffic statistics, port distribution, instances, and other details, by clicking the tabs across the top of the page.

`Figure 106`_ shows the **Summary** tab for an individual network, which displays connectivity details and traffic statistics for the selected network.

.. _Figure 106: 

*Figure 106* : Individual Network Connectivity Details—Summary Tab

.. figure:: s041874.gif

`Figure 107`_ shows the **Port Map** tab for an individual network, which displays the relative distribution of traffic for this network by protocol, by port.

.. _Figure 107: 

*Figure 107* : Individual Network-– Port Map Tab

.. figure:: s041875.gif

`Figure 108`_ shows the **Port Distribution** tab for an individual network, which displays the relative distribution of traffic in and out by source port and destination port.

.. _Figure 108: 

*Figure 108* : Individual Network-– Port Distribution Tab

.. figure:: s041876.gif

`Figure 109`_ shows the **Instances** tab for an individual network, which displays details for each instance associated with this network, including the number of interfaces, the associated vRouter, the instance IP address, and the volume of traffic in and out.

Additionally, you can click the arrow near the instance name to reveal even more details about the instance—the interfaces and their addresses, UUID, CPU (usage), and memory used of the total amount available.

.. _Figure 109: 

*Figure 109* : Individual Network Instances Tab

.. figure:: s041877.gif

`Figure 110`_ shows the **Details** tab for an individual network, which displays the code used to define this network -–the User Virtual Environment (UVE) code.

.. _Figure 110: 

*Figure 110* : Individual Network Details Tab

.. figure:: s041878.gif

