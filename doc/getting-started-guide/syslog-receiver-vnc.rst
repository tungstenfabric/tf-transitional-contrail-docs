.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

================================================
System Log Receiver in Tungsten Fabric Analytics
================================================

-  `Overview`_ 


-  `Redirecting System Logs to Tungsten Fabric Collector`_ 


-  `Exporting Logs from Tungsten Fabric Analytics`_ 



Overview
========

The contrail-collector process on the Tungsten Fabric Analytics node can act as a system log receiver.


Redirecting System Logs to Tungsten Fabric Collector
====================================================

You can enable the contrail-collector to receive system logs by giving a valid ``syslog_port`` as a command line option:
``--DEFAULT.syslog_port <arg>`` 
or by adding ``syslog_port`` in the DEFAULT section​ of the configuration file at ``/etc/contrail/contrail-collector.conf`` .
For nodes to send system logs to the contrail-collector, the system log configuration for the node should be set up to direct the system logs to contrail-collector.

Example
-------

Add the following line in ``/etc/rsyslog.d/50-default.conf`` on an Ubuntu system to redirect the system logs to contrail-collector.

::

	*.* @<collector_ip>:<collector_syslog_port> :: @ for udp, @@ for tcp

The logs can be retrieved by using Tungsten Fabric tool, either by using the contrail-logs utility on the analytics node or by using the Tungsten Fabric user interface on the system log query page.


Exporting Logs from Tungsten Fabric Analytics
=============================================

You can also export logs stored in Tungsten Fabric analytics to another system log receiver by using the ``contrail-logs`` utility.

The contrail-logs utility can take these options: ``--send-syslog, --syslog-server, --syslog-port,`` to query Tungsten Fabric analytics, then send the results as system logs to a system log server. This is an on-demand command, one can write a cron job or a job that continuously invokes ``contrail-logs`` to achieve continuous sending of logs to another system log server.

