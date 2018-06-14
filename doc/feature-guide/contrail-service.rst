.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================
service (Managing Services)
===========================

------
Syntax
------

 service *contrail-service* ( start | stop | restart | status )

-------------------
Release Information
-------------------

Standard Linux command used for managing and viewing services in Contrail Controller Release 1.0.

-----------
Description
-----------

Start, stop, or restart a Contrail service. Display the status of a Contrail service.

All contrail services are managed by the process ``supervisord`` , which is open source software written in Python. Each Contrail node type, such as compute, control, and so on, has an instance of ``supervisord`` that, when running, launches Contrail services as child processes. All ``supervisord`` instances display in ``contrail-status`` output with the prefix ``supervisor`` . If the ``supervisord`` instance of a particular node type is not up, none of the services for that node type are up. For more details about the open source ``supervisord`` process, see http://www.supervisord.org .

- start—start a named service.


- stop—stop a named service.


- restart—stop and restart a named service.


- status—display the status of a named service.


------------------------
Required Privilege Level
------------------------

admin

-------------
Sample Output
-------------

The following examples show usage for the ``contrail-collector`` service, which is only configured on nodes that have the roles of **analytics, configuration, web-ui** , or **database** .


Sample Output
-------------
::

 [root@host service supervisor-analytics status  
::

 supervisord (pid  32116) is running... [
::

 [root@host]# service contrail-collector restart 
::

    
 contrail-collector: stopped
 contrail-collector: started

::
 
[root@host]# service contrail-collector stop 
::


 contrail-collector: stopped

::

 [root@host]# service contrail-collector start 
::


 contrail-collector: started

::

 [root@host]# service contrail-collector status 
::


 contrail-collector               RUNNING    pid 20071, uptime 0:00:04


.. _http://www.supervisord.org: http://www.supervisord.org
