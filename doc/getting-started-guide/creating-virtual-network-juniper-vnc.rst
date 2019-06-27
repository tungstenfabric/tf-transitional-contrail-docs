.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===============================================
Creating a Virtual Network with Tungsten Fabric
===============================================

Tungsten Fabric makes creating a virtual network very easy for a self-service user. You create networks and network policies at the user dashboard, then associate policies with each network. The following procedure shows how to create a virtual network when using Tungsten Fabric.


#. You need to create an IP address management (IPAM) for your project for to create a virtual network. Select **Configure > Networking > IP Address Management** , then click the **Create** button.

   The **Add IP Address Management** window appears, see `Figure 17`_ .

   .. _Figure 17: 

   *Figure 17* : Add IP Address Management

   .. figure:: s041838.gif



#. Complete the fields in **Add IP Address Management** : The fields are described in `Table 4`_ .

   .. _Table 4: 

   *Table 4* : Add IP Address Management Fields

   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Field             | Description                                                                                           |
   +===================+=======================================================================================================+
   | Name              | Enter a name for the IPAM you are creating.                                                           |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | DNS Method        | Select from a list the domain name server method for this IPAM: Default, Virtual DNS, Tenant, or None.|
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | NTP Server IP     | Enter the IP address of an NTP server to be used for this IPAM.                                       |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Domain Name       | Enter a domain name to be used for this IPAM.                                                         |
   +-------------------+-------------------------------------------------------------------------------------------------------+


#. Select **Configure > Networking > Networks** to access the **Configure Networks** page; see `Figure 18`_ .

   .. _Figure 18: 

   *Figure 18* : Configure Networks

   .. figure:: s042492.png



#. Verify that your project is displayed as active in the upper-right field, then click the |s042494.png| icon. The **Create Network** window is displayed. See `Figure 19`_ . Use the scroll bar to access all sections of this window.

   .. _Figure 19: 

   *Figure 19* : Create Network

   .. figure:: s041528.gif



#. Complete the fields in the **Create Network** window with values that identify the network name, network policy, and IP options as needed. See field descriptions in `Table 5`_ .

   .. _Table 5: 


   *Table 5* : Create Network Fields

   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Field             | Description                                                                                                                         |
   +===================+=====================================================================================================================================+
   | Name              | Enter a name for the virtual network you are creating.                                                                              |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Network Policy    | Select the policy to be applied to this network from the list of available policies. You can select morethan one policy by clicking |
   |                   | each one needed.                                                                                                                    |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Subnets           | Use this area to identify and manage subnets for this virtual network. Click the + icon to open fields for IPAM, CIDR, Allocation   |
   |                   | Pools, Gateway, DNS, and DHCP. Select the subnet to be added from a drop down list in the IPAM field. Complete the remaining fields |
   |                   | as necessary. You can add multiple subnets to a network. When finished, click the + icon to add the selections into the columns     |
   |                   | below the fields. Alternatively, click the - icon to remove the selections.                                                         |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Host Routes       | Use this area to add or remove host routes for this network. Click the + icon to open fields where you can enter the Route Prefix   |
   |                   | the Next Hop, Click the + icon to add the information, or click the - icon. to remove the information.                              |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Advanced Options  | Use this area to add or remove advanced options, including identifying the Admin State as Up or Down, to identify the network       |
   |                   | as Shared or External, to add DNS servers, or to define a VxLAN Identifier.                                                         |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Floating IP Pools | Use this area to identify and manage the floating IP address pools for this virtual network. Click the + icon to open fields where  |
   |                   | can enter the Pool Name and Projects. Click the + icon to add the information, or click the - icon to remove the information.       |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Route Target      | Move the scroll bar down to access this area, then specify one or more route targets for this virtual network. Click the + icon to  |
   |                   | open fields where you can enter route target identifiers. Click the + icon to add the information, or click the - icon to remove the|
   |                   | information.                                                                                                                        |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------+



#. To save your network, click the **Save** button, or click **Cancel** to discard your work and start over.


Now you can create a network policy, see.

**Related Documentation**

-  `Creating an Image for a Project in OpenStack Tungsten Fabric`_ 

.. _Creating a Network Policy—Tungsten Fabric: 

.. _Creating an Image for a Project in OpenStack Tungsten Fabric: creating-image-vnc.html


.. |s042494.png| image:: s042494.png
