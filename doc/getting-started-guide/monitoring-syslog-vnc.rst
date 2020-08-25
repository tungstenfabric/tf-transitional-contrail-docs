.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

============
Query > Logs
============

The **Query > Logs** option allows you to access the system log and object log activity of any Tungsten Fabric Controller component from one central location.

-  `Query > Logs Menu Options`_ 


-  `Query > Logs > System Logs`_ 


-  `Sample Query for System Logs`_ 


-  `Query > Logs > Object Logs`_ 



Query > Logs Menu Options
=========================

Click **Query > Logs** to access the **Query Logs** menu, where you can select **System Logs** to view system log activity, **Object Logs** to view object logs activity, and **Query Queue** to create custom queries of log activity; see `Figure 121`_ .

.. _Figure 121: 

*Figure 121* : Query > Logs

.. figure:: s041893.gif


Query > Logs > System Logs
==========================

Click **Query > Logs > System Logs** to access the **Query System Logs** menu, where you can view system logs according to criteria that you determine. See `Figure 122`_ .

.. _Figure 122: 

*Figure 122* : Query > Logs > System Logs

.. figure:: s041894.gif

The query fields available on the **Query System Logs** screen are described in `Table 48`_ .

.. _Table 48: 


*Table 48* : Query System Logs Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Time Range**                    | Select a range of time for which  |
|                                   | to see the system logs:           |
|                                   |                                   |
|                                   | -  Last 10 Mins                   |
|                                   | -  Last 30 Mins                   |
|                                   | -  Last 1 Hr                      |
|                                   | -  Last 6 Hrs                     |
|                                   | -  Last 12 Hrs                    |
|                                   | -  Custom                         |
|                                   |                                   |
|                                   | If you click Custom, enter a      |
|                                   | desired time range in two new     |
|                                   | fields: **From Time** and **To    |
|                                   | Time**.                           |
+-----------------------------------+-----------------------------------+
| **Where**                         | Click the edit button (pencil     |
|                                   | icon) to open a query-writing     |
|                                   | window, where you can specify     |
|                                   | query values for variables such   |
|                                   | as Source, Module, MessageType,   |
|                                   | and the like, in order to         |
|                                   | retrieve specific information.    |
+-----------------------------------+-----------------------------------+
| **Level**                         | Select the message severity level |
|                                   | to view:                          |
|                                   |                                   |
|                                   | -  SYS_NOTICE                     |
|                                   | -  SYS_EMERG                      |
|                                   | -  SYS_ALERT                      |
|                                   | -  SYS_CRIT                       |
|                                   | -  SYS_ERR                        |
|                                   | -  SYS_WARN                       |
|                                   | -  SYS_INFO                       |
|                                   | -  SYS_DEBUG                      |
+-----------------------------------+-----------------------------------+
| **Run Query**                     | Click this button to retrieve the |
|                                   | system logs that match the query. |
|                                   | The logs are listed in a box with |
|                                   | columns showing the **Time**,     |
|                                   | **Source**, **Module Id**,        |
|                                   | **Category**, **Log Type**, and   |
|                                   | **Log** message.                  |
+-----------------------------------+-----------------------------------+
| **Export**                        | This button appears after you     |
|                                   | click **Run Query**, allowing you |
|                                   | to export the list of system      |
|                                   | messages to a text/csv file.      |
+-----------------------------------+-----------------------------------+

Sample Query for System Logs
============================

This section shows a sample system logs query designed to show all **System Logs** from ``ModuleId = VRouterAgent on Source = b1s16`` and filtered by **Level**  ``= SYS_DEBUG`` .


#. At the **Query System Logs** screen, click in the **Where** field to access the **Where** query screen and enter information defining the location to query in the **Edit Where Clause** section and click **OK** ; see `Figure 123`_ .

   .. _Figure 123: 

   *Figure 123* : Edit Where Clause

   .. figure:: s041895.gif



#. The information you defined at the Where screen displays on the **Query System Logs** . Enter any more defining information needed; see `Figure 124`_ . When finished, click **Run Query** to display the results.

   .. _Figure 124: 

   *Figure 124* : Sample Query System Logs

   .. figure:: s041896.gif



Query > Logs > Object Logs
==========================

Object logs allow you to search for logs associated with a particular object, for example, all logs for a specified virtual network. Object logs record information related to modifications made to objects, including creation, deletion, and other modifications; see `Figure 125`_ .

.. _Figure 125: 

*Figure 125* : Query > Logs > Object Logs

.. figure:: s041897.gif

The query fields available on the **Object Logs** screen are described in `Table 49`_ .

.. _Table 49: 


*Table 49* : Object Logs Query Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Time Range**                    | Select a range of time for which  |
|                                   | to see the logs:                  |
|                                   |                                   |
|                                   | -  Last 10 Mins                   |
|                                   | -  Last 30 Mins                   |
|                                   | -  Last 1 Hr                      |
|                                   | -  Last 6 Hrs                     |
|                                   | -  Last 12 Hrs                    |
|                                   | -  Custom                         |
|                                   |                                   |
|                                   | If you click Custom, enter a      |
|                                   | desired time range in two new     |
|                                   | fields: **From Time** and **To    |
|                                   | Time**.                           |
+-----------------------------------+-----------------------------------+
| **Object Type**                   | Select the object type for which  |
|                                   | to show logs:                     |
|                                   |                                   |
|                                   | -  Virtual Network                |
|                                   | -  Virtual Machine                |
|                                   | -  Virtual Router                 |
|                                   | -  BGP Peer                       |
|                                   | -  Routing Instance               |
|                                   | -  XMPP Connection                |
+-----------------------------------+-----------------------------------+
| **Object Id**                     | Select from a list of available   |
|                                   | identifiers the name of the       |
|                                   | object you wish to use.           |
+-----------------------------------+-----------------------------------+
| **Select**                        | Click the edit button (pencil     |
|                                   | icon) to open a window where you  |
|                                   | can select searchable types by    |
|                                   | clicking a checkbox:              |
|                                   |                                   |
|                                   | -  ObjectLog                      |
|                                   | -  SystemLog                      |
+-----------------------------------+-----------------------------------+
| **Where**                         | Click the edit button (pencil     |
|                                   | icon) to open the query-writing   |
|                                   | window, where you can specify     |
|                                   | query values for variables such   |
|                                   | as **Source**, **ModuleId**, and  |
|                                   | **MessageType**, in order to      |
|                                   | retrieve information as specific  |
|                                   | as you wish.                      |
+-----------------------------------+-----------------------------------+
| **Run Query**                     | Click this button to retrieve the |
|                                   | system logs that match the query. |
|                                   | The logs are listed in a box with |
|                                   | columns showing the **Time**,     |
|                                   | **Source**, **Module Id**,        |
|                                   | **Category**, **Log Type**, and   |
|                                   | **Log** message.                  |
+-----------------------------------+-----------------------------------+
| **Export**                        | This button appears after you     |
|                                   | click **Run Query**, allowing you |
|                                   | to export the list of system      |
|                                   | messages to a text/csv file.      |
+-----------------------------------+-----------------------------------+
