.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===============================================
Backing Up Contrail Databases Using JSON Format
===============================================

This document shows how to backup Contrail databases (Cassandra and Zookeeper) using a JSON format. Instructions are given for both non-containerized and containerized versions of Contrail, starting with Contrail 4.0.

-  `Preliminary Cautions`_ 


-  `Simple Backup Using JSON Format`_ 


-  `Restore Simple Database Backup`_ 


-  `Example Backup and Restore With JSON`_ 




Preliminary Cautions
--------------------


.. caution:: Because the state of the Contrail database is associated with other system databases, such as OpenStack databases, database backups must be consistent across all systems and database changes associated with northbound APIs must be stopped on all systems before performing any backup operation. For example, you might block the external VIP for northbound APIs at the load balancer level, such as HAproxy.





Simple Backup Using JSON Format
-------------------------------

Perform a simple backup (database dump). Working from a controller node, use ``db_json_exim.py`` , located at ``/usr/lib/python2.7/dist-packages/cfgm_common`` .


.. note:: The controller node for non-containerized Contrail is a virtual machine (VM).

          The controller node for containerized Contrail is a controller container.



``cd /usr/lib/python2.7/dist-packages/cfgm_common`` 

``python db_json_exim.py --export-to db-dump.json`` 

- To see a cleaner version of the dump.

``cat db-dump.json | python -m json.tool | less`` 


- To omit keyspace in the dump, for example, to share with Juniper.

``python db_json_exim.py --export-to db-dump.json --omit-keyspace dm_keyspace`` 




Restore Simple Database Backup
------------------------------

Use the following steps to restore a system from a simple backup.


#. Stop ``supervisor-config`` on all controllers, if present, or ensure it is already stopped.

    ``service supervisor-config stop`` 



#. Stop Cassandra on all ``config-db`` controllers or ensure it is already stopped.

    ``service cassandra stop`` 



#. Stop Zookeeper on all controllers or ensure it is already stopped.

    ``service zookeeper stop`` 



#. Stop Kafka on all controllers. Be sure to check analytics controllers.

    ``service kafka stop`` 



#. Stop ``contrail-hamon`` on all controllers, if it is running on controllers.

    ``service contrail-hamon stop`` 



#. Backup the Zookeeper data directory on all controllers.

    ``cd /var/lib/zookeeper/`` 

    ``cp -R version-2/ version-2-save`` 



#. Backup the Cassandra data directory on all controllers.

    ``cd /var/lib/`` 

    ``cp -R cassandra cassandra-save`` 



#. Wipe out the Zookeeper data directory contents on all controllers.

    ``rm -rf /var/lib/zookeeper/version-2/*`` 



#. Wipe out the Cassandra data directory contents on all controllers.

    ``rm -rf /var/lib/cassandra/*`` 



#. Start Zookeeper on all controllers.

    ``service zookeeper start`` 



#. Start Cassandra on all controllers.

    ``service cassandra start`` 



#. Run ``python db_json_exim.py --import-from db-dump.json`` on any one controller.

    ``cd /usr/lib/python2.7/dist-packages/cfgm_common`` 

    ``python db_json_exim.py --import-from db-dump.json`` 



#. Start ``supervisor-config`` on all controllers (if present).

    ``service supervisor-config start`` 



#. Start Kafka on all controllers (check in analytics controllers).

    ``service kafka start`` 



#. Start ``contrail-hamon`` on all controllers, if previously stopped.

    ``service contrail-hamon start`` 




Example Backup and Restore With JSON
------------------------------------

This section provides an example of a simple database backup and restore of a system that has three controllers with config-db and separate IPs with the following host IDs:

- 5b5s42


- 5b5s43


- 5b5s44




Example: Perform Simple Backup
------------------------------
::

 root@5b5s42:~# python db_json_exim.py --export-to db-dump.json
 root@5b5s42:~# cat db-dump.json | python -m json.tool | less
  {
      "cassandra": {
          "config_db_uuid": {
         "obj_fq_name_table": {
                  "access_control_list": {
                  
   <snip>



Example: Perform Restore
------------------------


#. Stop ``supervisor-config`` on all controllers, if present.

   ::

    Non-Containerized Version: root@5b5s42:~# service supervisor-config stop
    supervisor-config stop/waiting
    root@5b5s42:~#
    root@5b5s43:~# service supervisor-config stop
    supervisor-config stop/waiting
    root@5b5s43:~#
    root@5b5s44:~# service supervisor-config stop
    supervisor-config stop/waiting
    root@5b5s44:~#

   ::

    Containerized Version:
    root@host-4.1:~# docker ps
    CONTAINER ID        IMAGE                                                          COMMAND                  CREATED             STATUS              PORTS               NAMES
    8802395bc033        172.30.109.59:5100/contrail410-contrail-analytics:mainline     "/lib/systemd/syst..."   7 weeks ago         Up 2 weeks                              analytics
    f5aed0a2efc3        172.30.109.59:5100/contrail410-contrail-analyticsdb:mainline   "/lib/systemd/syst..."   7 weeks ago         Up 2 weeks                              analyticsdb
    0ff200b12112        172.30.109.59:5100/contrail410-contrail-controller:mainline    "/lib/systemd/syst..."   7 weeks ago         Up 2 weeks                              controller
    6fec888f8145        registry:2                                                     "/entrypoint.sh /e..."   7 weeks ago         Up 2 weeks                              registry
    root@host-4.1:~# docker exec -it 0ff200b12112  /bin/bash




#. Stop Cassandra on all controllers.

   ::

    root@5b5s42:~# service cassandra stop
    root@5b5s42:~#
    root@5b5s43:~# service cassandra stop
    root@5b5s43:~#
    root@5b5s44:~# service cassandra stop
    root@5b5s44:~#



#. Stop Zookeeper on all controllers.

   ::

    root@5b5s42:~# service zookeeper stop
    zookeeper stop/waiting
    root@5b5s42:~#
    root@5b5s43:~# service zookeeper stop
    zookeeper stop/waiting
    root@5b5s43:~#
    root@5b5s44:~# service zookeeper stop
    zookeeper stop/waiting
    root@5b5s44:~#



#. Stop Kafka on all controllers.

   ::

    root@5b5s42:~# service kafka stop
    kafka: stopped
    root@5b5s42:~#
    root@5b5s43:~# service kafka stop
    kafka: stopped
    root@5b5s43:~#
    root@5b5s44:~# service kafka stop
    kafka: stopped
    root@5b5s44:~#



#. Stop ``contrail-hamon`` on all controllers, if present.
   ::

    root@5b5s42:~# service contrail-hamon stop
    contrail-hamon stop/waiting
    root@5b5s43:~# service contrail-hamon stop
    contrail-hamon stop/waiting
    root@5b5s44:~# service contrail-hamon stop
    contrail-hamon stop/waiting



#. Backup the Zookeeper data directory on all controllers.
   ::

    root@5b5s42:~# cd /var/lib/zookeeper/
    root@5b5s42:/var/lib/zookeeper# cp -R version-2/ version-2-save
    root@5b5s42:/var/lib/zookeeper#
    root@5b5s43:~# cd /var/lib/zookeeper/
    root@5b5s43:/var/lib/zookeeper# cp -R version-2/ version-2-save
    root@5b5s43:/var/lib/zookeeper#
    root@5b5s44:~# cd /var/lib/zookeeper/
    root@5b5s44:/var/lib/zookeeper# cp -R version-2/ version-2-save
    root@5b5s44:/var/lib/zookeeper#



#. Backup the Cassandra data directory on all controllers.
   ::

    root@5b5s42:~# cd /var/lib/
    root@5b5s42:/var/lib# cp -R cassandra cassandra-save
    root@5b5s42:/var/lib#
    root@5b5s43:~# cd /var/lib/
    root@5b5s43:/var/lib# cp -R cassandra cassandra-save
    root@5b5s43:/var/lib#
    root@5b5s44:~# cd /var/lib/
    root@5b5s44:/var/lib# cp -R cassandra/ cassandra-save
    root@5b5s44:/var/lib#



#. Wipe out the Zookeeper data directory contents on all controllers.
   ::

    root@5b5s42:~# rm -rf /var/lib/zookeeper/version-2/*
    root@5b5s42:~#
    root@5b5s43:~# rm -rf /var/lib/zookeeper/version-2/*
    root@5b5s43:~#
    root@5b5s44:~# rm -rf /var/lib/zookeeper/version-2/*
    root@5b5s44:~#



#. Wipe out the Cassandra data directory contents on all controllers.
   ::

    root@5b5s42:~# rm -rf /var/lib/cassandra/*
    root@5b5s42:~#
    root@5b5s43:~# rm -rf /var/lib/cassandra/*
    root@5b5s43:~#
    root@5b5s44:~# rm -rf /var/lib/cassandra/*
    root@5b5s44:~# 



#. Start Zookeeper on all controllers.
   ::

    root@5b5s42:~# service zookeeper start
    zookeeper start/running, process 14180
    root@5b5s42:~#
    root@5b5s43:~# service zookeeper start
    zookeeper start/running, process 11635
    root@5b5s43:~#
    root@5b5s44:~# service zookeeper start
    zookeeper start/running, process 28040
    root@5b5s44:~#



#. Start Cassandra on all controllers.
   ::

     root@5b5s42:~# service cassandra start
     root@5b5s42:~#
     root@5b5s43:~# service cassandra start
     root@5b5s43:~#
     root@5b5s44:~# service cassandra start
     root@5b5s44:~#



#. Run ``python db_json_exim.py --import-from db-dump.json`` on any *one* controller.
   ::

    root@5b5s42:~# python db_json_exim.py --import-from db-dump.json
    root@5b5s42:~#



#. Start ``supervisor-config`` on all controllers, if present.
   ::

    root@5b5s42:~# service supervisor-config start
    supervisor-config start/running, process 19286
    root@5b5s42:~#
    root@5b5s43:~# service supervisor-config start
    supervisor-config start/running, process 28937
    root@5b5s43:~#
    root@5b5s44:~# service supervisor-config start
    supervisor-config start/running, process 21242
    root@5b5s44:~#



#. Start Kafka on all controllers.
   ::

    root@5b5s42:~# service kafka start
    kafka: started
    root@5b5s42:~#
    root@5b5s43:~# service kafka start
    kafka: started
    root@5b5s43:~#
    root@5b5s44:~# service kafka start
    kafka: started
    root@5b5s44:~#



#. Start ``contrail-hamon`` on all controllers, if present.
   ::

    root@5b5s42:~# service contrail-hamon start
    contrail-hamon start/running, process 1379
    root@5b5s42:~#
    root@5b5s43:~# service contrail-hamon start
    contrail-hamon start/running, process 1230
    root@5b5s43:~#
    root@5b5s44:~# service contrail-hamon start
    contrail-hamon start/running, process 26843
    root@5b5s44:~#


