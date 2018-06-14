.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==========================================
Monitor > Infrastructure > Analytics Nodes
==========================================

Select **Monitor > Infrastructure > Analytics Nodes** to view the console logs, generators, and query expansion (QE) queries of the analytics nodes.

-  `Monitor Analytics Nodes`_ 


-  `Monitor Analytics Individual Node Details Tab`_ 


-  `Monitor Analytics Individual Node Generators Tab`_ 


-  `Monitor Analytics Individual Node QE Queries Tab`_ 


-  `Monitor Analytics Individual Node Console Tab`_ 



Monitor Analytics Nodes
=======================

Select **Monitor > Infrastructure > Analytics Nodes** to view a summary of activities for the analytics nodes; see `Figure 186`_ . See `Table 52`_ for descriptions of the fields on the analytics summary.

.. _Figure 186: 

*Figure 186* : Analytics Nodes Summary

.. figure:: s041517.gif

.. _Table 52: 


*Table 52* : Fields on Analytics Nodes Summary

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Host name**                     | The name of this node.            |
+-----------------------------------+-----------------------------------+
| **IP address**                    | The IP address of this node.      |
+-----------------------------------+-----------------------------------+
| **Version**                       | The version of software installed |
|                                   | on the system.                    |
+-----------------------------------+-----------------------------------+
| **Status**                        | The current operational status of |
|                                   | the node — Up or Down — and the   |
|                                   | length of time it is in that      |
|                                   | state.                            |
+-----------------------------------+-----------------------------------+
| **CPU (%)**                       | The average CPU percentage usage  |
|                                   | for this node.                    |
+-----------------------------------+-----------------------------------+
| **Memory**                        | The average memory usage for this |
|                                   | node.                             |
+-----------------------------------+-----------------------------------+
| **Generators**                    | The total number of generators    |
|                                   | for this node.                    |
+-----------------------------------+-----------------------------------+


Monitor Analytics Individual Node Details Tab
=============================================

Click the name of any analytics node displayed on the analytics summary to view the **Details** tab for that node. See `Figure 187`_ .

See `Table 53`_ for descriptions of the fields on this screen.

.. _Figure 187: 

*Figure 187* : Monitor Analytics Individual Node Details Tab

.. figure:: s041518.gif

.. _Table 53: 


*Table 53* : Monitor Analytics Individual Node Details Tab Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Hostname**                      | The name of this node.            |
+-----------------------------------+-----------------------------------+
| **IP Address**                    | The IP address of this node.      |
+-----------------------------------+-----------------------------------+
| **Version**                       | The installed version of the      |
|                                   | software.                         |
+-----------------------------------+-----------------------------------+
| **Overall Node Status**           | The current operational status of |
|                                   | the node — Up or Down — and the   |
|                                   | length of time in this state.     |
+-----------------------------------+-----------------------------------+
| **Processes**                     | The current status of each        |
|                                   | analytics process, including      |
|                                   | Collector, Query Engine, and      |
|                                   | OpServer.                         |
+-----------------------------------+-----------------------------------+
| **CPU (%)**                       | The average CPU percentage usage  |
|                                   | for this node.                    |
+-----------------------------------+-----------------------------------+
| **Memory**                        | The average memory usage of this  |
|                                   | node.                             |
+-----------------------------------+-----------------------------------+
| **Messages**                      | The total number of messages for  |
|                                   | this node.                        |
+-----------------------------------+-----------------------------------+
| **Generators**                    | The total number of generators    |
|                                   | associated with this node.        |
+-----------------------------------+-----------------------------------+
| **Last Log**                      | The date and time of the last log |
|                                   | message issued about this node.   |
+-----------------------------------+-----------------------------------+


Monitor Analytics Individual Node Generators Tab
================================================

The **Generators** tab displays information about the generators for an individual analytics node; see `Figure 188`_ . Click the expansion arrow next to any generator name to reveal more details. See `Table 54`_ for descriptions of the fields on the **Peers** tab screen.

.. _Figure 188: 

*Figure 188* : Individual Analytics Node—Generators Tab

.. figure:: s041523.gif

.. _Table 54: 


*Table 54* : Monitor Analytics Individual Node Generators Tab Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Name**                          | The host name of the generator.   |
+-----------------------------------+-----------------------------------+
| **Status**                        | The current status of the peer—   |
|                                   | Up or Down — and the length of    |
|                                   | time in that state.               |
+-----------------------------------+-----------------------------------+
| **Messages**                      | The number of messages sent and   |
|                                   | received from this peer.          |
+-----------------------------------+-----------------------------------+
| **Bytes**                         | The total message size in bytes.  |
+-----------------------------------+-----------------------------------+


Monitor Analytics Individual Node QE Queries Tab
================================================

The **QE Queries** tab displays the number of query expansion (QE) messages that are in the queue for this analytics node. See `Figure 189`_ .

See `Table 55`_ for descriptions of the fields on the **QE Queries** tab screen.

.. _Figure 189: 

*Figure 189* : Individual Analytics Node—QE QueriesTab

.. figure:: s041524.gif

.. _Table 55: 


*Table 55* : Analytics Node QE Queries Tab Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Enqueue Time**                  | The length of time this message   |
|                                   | has been in the queue waiting to  |
|                                   | be delivered.                     |
+-----------------------------------+-----------------------------------+
| **Query**                         | The query message.                |
+-----------------------------------+-----------------------------------+
| **Progress (%)**                  | The percentage progress for the   |
|                                   | message delivery.                 |
+-----------------------------------+-----------------------------------+


Monitor Analytics Individual Node Console Tab
=============================================

Click the **Console** tab for an individual analytics node to display system logging information for a defined time period. See `Figure 190`_ . See `Table 56`_ for descriptions of the fields on the **Console** tab screen.

.. _Figure 190: 

*Figure 190* : Analytics Individual Node—Console Tab

.. figure:: s041519.png

.. _Table 56: 


*Table 56* : Monitor Analytics Individual Node Console Tab Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Time Range**                    | Select a timeframe for which to   |
|                                   | review logging information as     |
|                                   | sent to the console. There are 11 |
|                                   | options, ranging from the **Last  |
|                                   | 5 mins** through to the **Last 24 |
|                                   | hrs**. The default display is for |
|                                   | the **Last 5 mins**.              |
+-----------------------------------+-----------------------------------+
| **Log Category**                  | Select a log category to display: |
|                                   |                                   |
|                                   | -  All                            |
|                                   |                                   |
|                                   | -  \_default\_                    |
|                                   |                                   |
|                                   | -  XMPP                           |
|                                   |                                   |
|                                   | -  TCP                            |
+-----------------------------------+-----------------------------------+
| **Log Type**                      | Select a log type to display.     |
+-----------------------------------+-----------------------------------+
| **Log Level**                     | Select a log severity level to    |
|                                   | display:                          |
|                                   |                                   |
|                                   | -  SYS_EMERG                      |
|                                   |                                   |
|                                   | -  SYS_ALERT                      |
|                                   |                                   |
|                                   | -  SYS_CRIT                       |
|                                   |                                   |
|                                   | -  SYS_ERR                        |
|                                   |                                   |
|                                   | -  SYS_WARN                       |
|                                   |                                   |
|                                   | -  SYS_NOTICE                     |
|                                   |                                   |
|                                   | -  SYS_INFO                       |
|                                   |                                   |
|                                   | -  SYS_DEBUG                      |
+-----------------------------------+-----------------------------------+
| **Keywords**                      | Enter any text string to search   |
|                                   | for and display logs containing   |
|                                   | that string.                      |
+-----------------------------------+-----------------------------------+
| (Limit field)                     | Select the number of messages to  |
|                                   | display:                          |
|                                   |                                   |
|                                   | -  No Limit                       |
|                                   |                                   |
|                                   | -  Limit 10 messages              |
|                                   |                                   |
|                                   | -  Limit 50 messages              |
|                                   |                                   |
|                                   | -  Limit 100 messages             |
|                                   |                                   |
|                                   | -  Limit 200 messages             |
|                                   |                                   |
|                                   | -  Limit 500 messages             |
+-----------------------------------+-----------------------------------+
| **Auto Refresh**                  | Click the check box to            |
|                                   | automatically refresh the display |
|                                   | if more messages occur.           |
+-----------------------------------+-----------------------------------+
| **Display Logs**                  | Click this button to refresh the  |
|                                   | display if you change the display |
|                                   | criteria.                         |
+-----------------------------------+-----------------------------------+
| **Reset**                         | Click this button to clear any    |
|                                   | selected display criteria and     |
|                                   | reset all criteria to their       |
|                                   | default settings.                 |
+-----------------------------------+-----------------------------------+
| **Time**                          | This column lists the time        |
|                                   | received for each log message     |
|                                   | displayed.                        |
+-----------------------------------+-----------------------------------+
| **Category**                      | This column lists the log         |
|                                   | category for each log message     |
|                                   | displayed.                        |
+-----------------------------------+-----------------------------------+
| **Log Type**                      | This column lists the log type    |
|                                   | for each log message displayed.   |
+-----------------------------------+-----------------------------------+
| **Log**                           | This column lists the log message |
|                                   | for each log displayed.           |
+-----------------------------------+-----------------------------------+

