.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

====================================
Monitor > Infrastructure > Dashboard
====================================

Use **Monitor > Infrastructure > Dashboard** to get an “at-a-glance” view of the system infrastructure components, including the numbers of virtual routers, control nodes, analytics nodes, and config nodes currently operational, a bubble chart of virtual routers showing the CPU and memory utilization, log messages, system information, and alerts.

-  `Monitor Dashboard`_ 


-  `Monitor Individual Details from the Dashboard`_ 


-  `Using Bubble Charts`_ 


-  `Color-Coding of Bubble Charts`_ 



Monitor Dashboard
=================

Click **Monitor > Infrastructure > Dashboard** on the left to view the **Dashboard** . See `Figure 170`_ .

.. _Figure 170: 

*Figure 170* : Monitor > Infrastructure > Dashboard

.. figure:: s041572.gif


Monitor Individual Details from the Dashboard
=============================================

Across the top of the **Dashboard** screen are summary boxes representing the components of the system that are shown in the statistics. See `Figure 171`_ . Any of the control nodes, virtual routers, analytics nodes, and config nodes can be monitored individually and in detail from the **Dashboard** by clicking an associated box, and drilling down for more detail.

.. _Figure 171: 

*Figure 171* : Dashboard Summary Boxes

.. figure:: s041566.gif

Detailed information about monitoring each of the areas represented by the boxes is provided in the links in `Table 38`_ .

.. _Table 38: 


*Table 38* : Dashboard Summary Boxes

+---------------------+-----------------------------------------------+
| Box                 | For More Information                          |
+=====================+===============================================+
| **vRouters**        | `Monitor > Infrastructure > Virtual Routers`_ |
+---------------------+-----------------------------------------------+
| **Control Nodes**   | `Monitor > Infrastructure > Control Nodes`_   |
+---------------------+-----------------------------------------------+
| **Analytics Nodes** | `Monitor > Infrastructure > Analytics Nodes`_ |
+---------------------+-----------------------------------------------+
| **Config Nodes**    | `Monitor > Infrastructure > Config Nodes`_    |
+---------------------+-----------------------------------------------+


Using Bubble Charts
===================

Bubble charts show the CPU and memory utilization of components contributing to the current analytics display, including vRouters, control nodes, config nodes, and the like. You can hover over any bubble to get summary information about the component it represents; see `Figure 172`_ . You can click through the summary information to get more details about the component.

.. _Figure 172: 

*Figure 172* : Bubble Summary Information

.. figure:: s041898.gif


Color-Coding of Bubble Charts
=============================

Bubble charts use the following color-coding scheme:

*Control Nodes* 

  - Blue—working as configured.


  - Red—error, at least one configured peer is down.


*vRouters* 

  - Blue—working, but no instance is launched.


  - Green—working with at least one instance launched.


  - Red—error, there is a problem with connectivity or a vRouter is in a failed state.


**Related Documentation**

-  `Monitor > Infrastructure > Virtual Routers`_ 

-  `Monitor > Infrastructure > Control Nodes`_ 

-  `Monitor > Infrastructure > Analytics Nodes`_ 

-  `Monitor > Infrastructure > Config Nodes`_ 

.. _Monitor > Infrastructure > Virtual Routers: monitoring-vrouters-vnc.html

.. _Monitor > Infrastructure > Control Nodes: monitoring-infrastructure-vnc.html

.. _Monitor > Infrastructure > Analytics Nodes: monitor-analytics-vnc.html

.. _Monitor > Infrastructure > Config Nodes: monitor-config-vnc.html

.. _Monitor > Infrastructure > Virtual Routers: monitoring-vrouters-vnc.html

.. _Monitor > Infrastructure > Control Nodes: monitoring-infrastructure-vnc.html

.. _Monitor > Infrastructure > Analytics Nodes: monitor-analytics-vnc.html

.. _Monitor > Infrastructure > Config Nodes: monitor-config-vnc.html

