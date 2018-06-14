.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

======================================================
Integrating Contrail with VMware vRealize Orchestrator
======================================================

Starting in Contrail Release 5.0, a Beta version is provided of a dedicated Contrail plugin to connect to VMware vRealize Orchestrator (vRO). You can use the Contrail plugin to view the Contrail controller configuration in the vRO inventory and to modify configurations by using vRO workflows. You can also create network policies, security groups, and automate both simple and complex workflows by using vRO.

-  `Components of vRealize Orchestrator`_ 


-  `Contrail Workflows`_ 


-  `Deploying Contrail vRO Plugin`_ 




Components of vRealize Orchestrator
-----------------------------------

vRO consists of the following components:

- vRO Inventory—The vRO inventory displays the Contrail plugin and the Contrail node or endpoint. All Contrail plugin objects that represent your system are displayed in the vRO Inventory. Objects are displayed in a hierarchical order and are based on the Contrail schema.

  With Release 5.0, Contrail inventory objects such as projects, security groups, virtual networks, network IPAMs, network policies, ports, floating IP pools, and service templates are displayed in the vRO inventory. Relevant API objects are also displayed in the vRO inventory.


- vRO Workflows—The vRO workflow is a process that manipulates objects in a vRO Inventory. Each plugin has a set of predefined workflows. vRO combines workflows from different plugins to create complex processes and manages them. Multiple workflows are used to create blueprints in vRA.


.. note:: VMware vCenter plugin workflows are represented as simple workflows in vRO plugin. For more information on Contrail integration with VMware vCenter, see `Installing and Provisioning VMware vCenter with Containerized Contrail`_ .






Contrail Workflows
------------------

You must connect to the Contrail controller or an endpoint before you create Contrail workflows. You use **Create Contrail controller connection** to connect to an endpoint. Alternatively, you use **Delete Contrail controller connection** to terminate a connection with an endpoint. Once you connect to the Control controller, the vRO plugin accesses the Contrail inventory objects and then updates the vRO inventory with the Contrail inventory objects.

The following workflows are defined for simple networking operations:

- Network

- Create network


- Delete network



.. note:: You use the **Create network** workflow to create a network on the Contrail controller.


- Network Policy

    - Create network policy


    - Add rule to network policy


    - Remove network policy rule


    - Delete network policy



  - Security policy

    - Create security group


    - Add rule to security group


    - Edit security group


    - Remove security group rule


    - Delete security group



  - Service Instance

    - Add port tuple to service instance


    - Create service instance


    - Delete service instance


    - Remove port tuple from service instance



  - Network IPAM


  - Port


  - Project


  - Service Template


  - Virtual Network


  - Floating IP

    - Create floating IP


    - Delete floating IP



  - Floating IP pools

    - Create floating IP pool


    - Delete floating IP pool


    - Edit floating IP pool





Deploying Contrail vRO Plugin
-----------------------------

You can deploy the Contrail plugin in any Java Virtual Machine (JVM) compatible environment and load it on an active vRO instance.

For more information, see. `Installing and Provisioning Contrail VMware vRealize Orchestrator Plugin`_

.. _Installing and Provisioning VMware vCenter with Containerized Contrail: vcenter-integration-vnc-401.html

.. _Installing and Provisioning Contrail VMware vRealize Orchestrator Plugin: https://uat.juniper.net/documentation/test/en_US/contrail/topics/task/installation/install-contrail-vRO-plugin.html

