.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=========================================================
Creating a Virtual Network with OpenStack Tungsten Fabric
=========================================================

Tungsten Fabric makes creating a virtual network very easy for you. You create networks and network policies at the user dashboard, then associate policies with each network. The following procedure shows how to create a virtual network when using OpenStack.


#. To create a virtual network when using OpenStack Tungsten Fabric, select **Project > Other > Networking** . The **Networks** window is displayed. See `Figure 20`_ .

   .. _Figure 20: 

   *Figure 20* : Networks Window

   .. figure:: s041525.gif



#. Verify that the correct project is displayed in the **Current Project** box, then click **Create Network** . The **Create Network** window is displayed. See `Figure 21`_ and `Figure 22`_ .

   .. _Figure 21: 

   *Figure 21* : Create Network Window

   .. figure:: s018523.png

   .. _Figure 22: 

   *Figure 22* : Create Network Window Subnet Tab

   .. figure:: s018524.png



#. Click the **Network** , **Subnet** , **Subnet Detail** , and **Associate Network Policies** tabs to complete the fields in the **Create Network** window. See field descriptions in `Table 6`_ .

   .. _Table 6: 


   *Table 6* : Create Network Fields

   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Field             | Description                                                                                           |
   +===================+=======================================================================================================+
   | Network Name      | Enter a name for the network.                                                                         |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Subnet Name       | Enter a name for the subnetwork.                                                                      |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | IPAM              | Select the IPAM associated with the IP block.                                                         |
   |                   | For new projects, an IPAM can be added while creating the virtual network. VM instances created in    |
   |                   | this virtual network are assigned an address from this address block automatically by the system      |
   |                   | when a VM is launched.                                                                                |  
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Network Address   | Enter the network address in CIDR format.                                                             |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | IP Version*       | Select IPv4 or IPv6.                                                                                  |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Gateway IP        | Optionally, enter an explicit gateway IP address for the IP address block. Check the Disable          |
   |                   | Gateway box if no gateway is to be used.                                                              |
   +-------------------+-------------------------------------------------------------------------------------------------------+
   | Network Policy    | Any policies already created are listed. To select a policy, click the check box for the policy.      |
   +-------------------+-------------------------------------------------------------------------------------------------------+



#. Click the **Subnet Details** tab to specify the Allocation Pool, DNS Name Servers, and Host Routes.



#. Click the **Associate Network Policies** tab to associate policies to the network.



#. To save your network, click **Create Network** , or click **Cancel** to discard your work and start over.


