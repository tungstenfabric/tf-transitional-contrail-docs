.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============
Alarms History
==============

Starting with Contrail Release 4.0, you can view a history of alarms that were raised or reset. You can also view a history of user-visible entities (UVEs) that have been changed.

-  `Viewing Alarms History`_ 




Viewing Alarms History
----------------------

In the Contrail Web user interface, new fields at **Monitor > Alarms > Dashboard > Alarms History** now display alarms history, including alarms that were set or reset. `Figure 161`_ shows the alarms history, identifying the volume and types of alarms by time and the node types in which events are occurring. The right side panel lists by name the nodes in which active events are occurring.

You can also use a ``contrail-status`` query to view the alarms history. Additionally, the ``contrail-status`` displays a history of added, updated, and removed information for UVEs in Contrail.

.. _Figure 161: 

*Figure 161* : Alarms History Page

.. figure:: s019896.png

Tooltips are available on the Alarms History page. In the Events area, you can click on any node type listed to display a tooltip showing details of the events that have been added and cleared in that node, see 

`Figure 162`_ .

.. _Figure 162: 

*Figure 162* : Events Log Tooltip

.. figure:: s019897.png

You can expand the event log in the right side panel to display a detailed event log. Click the name of any node in the list in the right panel, and the details of the current alarms are visible in the expanded view, see `Figure 163`_ .

.. _Figure 163: 

*Figure 163* : Detailed Event Log

.. figure:: s019898.png

**Related Documentation**

-  `User Configuration for Analytics Alarms and Log Statistics`_ 

.. _User Configuration for Analytics Alarms and Log Statistics: analytics-user-alarms-log-statistics.html

