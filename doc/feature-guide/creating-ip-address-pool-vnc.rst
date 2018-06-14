.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===================================
Creating a Floating IP Address Pool
===================================

A floating IP address is an IP address (typically public) that can be dynamically assigned to a running virtual instance.

To configure floating IP address pools in project networks in Contrail, then allocate floating IP addresses from the pool to virtual machine instances in other virtual networks:


#. Select **Configure > Networking > Networks** ; see `Figure 60`_ . Make sure your project is the active project in the upper right.

   .. _Figure 60: 

   *Figure 60* : Configure > Networking > Networks

   .. figure:: s018527.png



#. Click the network you want to associate with a floating IP pool, then in the **Action** column, click the action icon and select **Edit** .

   The **Edit Network** window for the selected network is displayed; see `Figure 61`_ .

   .. _Figure 61: 

   *Figure 61* : Edit Network

   .. figure:: s018528.png



#. In the **Floating IP Pools** section, click the **Pool Name** field, enter a name for your floating IP pool, and click the **+** (plus sign) to add the IP pool to the table below the field.

   - Multiple floating IP pools can be created at the same time.


   - A floating IP pool can be associated with multiple projects.




#. Click **Save** to create the floating IP address pool, or click **Cancel** to remove your work and start over.


