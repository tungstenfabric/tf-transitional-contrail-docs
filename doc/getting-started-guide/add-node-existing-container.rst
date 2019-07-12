.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

======================================================================
Adding a New Node to an Existing Containerized Tungsten Fabric Cluster
======================================================================

This is the initial process for adding a new node to an existing cluster in containerized Tungsten Fabric.

-  `Controller Configuration`_ 

Controller Configuration
------------------------


#. Create contrailctl configuration and start a controller container on a new node.

   - Configure contrailctl configurations in /etc/contrailctl/controller.conf .

     See examples on github at:

      `contrail-docker/tools/python-contrailctl/examples/configs/controller.conf`_  


   - Start the controller container. For more information, see `How to run Tungsten Fabric Docker containers`_  .


   - Wait for the new containers to come up completely.




#. Configure the existing cluster nodes with new nodes.

   The purpose of this step is to reconfigure the existing cluster application configurations to include newly added servers, then restart to accommodate the configuration changes.


You can do this by using one of two methods described below:

-  `Using contrailctl to add node configuration on existing containers`_ 


-  `Manually configure contrailctl on all containers and sync the configs`_ 




Using contrailctl to add node configuration on existing containers
------------------------------------------------------------------

You can use contrailctl to add the node configuration on existing containers by running the following steps on all existing containers on all cluster nodes.


.. note:: Run this step first on all zookeeper *follower* nodes, then run on the leader node.




#. Determine which node is the leader node.

   To determine which node is the leader and which are followers in a zookeeper cluster, run the following commands against your zookeeper cluster nodes.

   ``$ echo stat | nc 192.168.0.102 2181 | grep Mode Mode: leader`` 

   ``$ echo stat | nc 192.168.0.100 2181 | grep Mode Mode: follower`` 



#. Run contrailctl on all the existing containers in all cluster nodes, follower nodes first and leader node last.

   ::

    $ contrailctl config node add -h 
    usage: contrailctl config node add [-h] -t {controller,analyticsdb,analytics}
                                       -n NODE_ADDRESSES [-s SEED_LIST]
                                       [-f CONFIG_FILE] -c
                                       {controller,analyticsdb,analytics,agent,lb,kubemanager,mesosmanager}
                                       [--config-list CONFIG_LIST]
    optional arguments:
      -h, --help            show this help message and exit
      -t {controller,analyticsdb,analytics}, --type {controller,analyticsdb,analytics}
                            Type of node
      -n NODE_ADDRESSES, --node-addresses NODE_ADDRESSES
                            Comma separated list of node addresses
      -s SEED_LIST, --seed-list SEED_LIST
                            Comma separated list of seed nodes to be used
      -f CONFIG_FILE, --config-file CONFIG_FILE
                            Master config file path
      -c {controller,analyticsdb,analytics,agent,lb,kubemanager,mesosmanager}, --component {controller,analyticsdb,analytics,agent,lb,kubemanager,mesosmanager}
                            contrail role to be configured
      --config-list CONFIG_LIST
                            comma separated list of config nodes. Optional it is
                            needed only when the new controller nodes added are
                            config service disabled

    # Add new controllers in analytics container
    $ contrailctl config node add -t controller -n 192.168.0.10,192.168.0.11 -s 192.168.0.102,192.168.0.99 -c analytics

    # Add new controllers in analyticsdb container
    $ contrailctl config node add -t controller -n 192.168.0.10,192.168.0.11 -s 192.168.0.102,192.168.0.99 -c analyticsdb

    # Add new controllers in other controller containers
    $ contrailctl config node add -t controller -n 192.168.0.10,192.168.0.11 -s 192.168.0.102,192.168.0.99 -c controller





Manually configure contrailctl on all containers and sync the configs
---------------------------------------------------------------------


#. Determine which node is the leader node.

   To determine which node is the leader and which are followers in a zookeeper cluster, run the following commands against your zookeeper cluster nodes.

   ``$ echo stat | nc 192.168.0.102 2181 | grep Mode Mode: leader`` 

   ``$ echo stat | nc 192.168.0.100 2181 | grep Mode Mode: follower`` 



#. Manually configure /etc/contrailctl/controller.conf with new nodes for various \*\._list configurations and config_seed_list. See examples at:

   https://github.com/Juniper/contrail-docker/blob/master/tools/python-contrailctl/examples/configs/controller.conf 



#. Run contrailctl within the containers.

   ``$ docker exec <container name> contrailctl config sync -c <component name>`` 

   ``$ docker exec controller contrailctl config sync -c controller`` 


Removing Nodes in an Existing Containerized Cluster
---------------------------------------------------

For the first version of containerized Tungsten Fabric, there is no script available for removing a node from an existing cluster. If it is necessary to remove a node from an existing containerized Tungsten Fabric cluster, please contact Juniper Networks JTAC for assistance.


.. _contrail-docker/tools/python-contrailctl/examples/configs/controller.conf: https://github.com/Juniper/contrail-docker/blob/master/tools/python-contrailctl/examples/configs/controller.conf

.. _How to run Tungsten Fabric Docker containers: https://github.com/Juniper/contrail-docker/wiki/How-to-run-contrail-docker-containers

.. _https://github.com/Juniper/contrail-docker/blob/master/tools/python-contrailctl/examples/configs/controller.conf: https://github.com/Juniper/contrail-docker/blob/master/tools/python-contrailctl/examples/configs/controller.conf
