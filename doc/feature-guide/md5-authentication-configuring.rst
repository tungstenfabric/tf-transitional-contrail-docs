.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===============================================
Configuring MD5 Authentication for BGP Sessions
===============================================

Contrail supports MD5 authentication for BGP peering based on RFC 2385.

This option allows BGP to protect itself against the introduction of spoofed TCP segments into the connection stream. Both of the BGP peers must be configured with the same MD5 key. Once configured, each BGP peer adds a 16-byte MD5 digest to the TCP header of every segment that it sends. This digest is produced by applying the MD5 algorithm on various parts of the TCP segment. Upon receiving a signed segment, the receiver validates it by calculating its own digest from the same data (using its own key) and compares the two digests. For valid segments, the comparison is successful since both sides know the key.

The following are ways to enable BGP MD5 authentication and set the keys on the Contrail node.


#. If the ``md5`` key is not included in the provisioning, and the node is already provisioned, you can run the following script with an argument for md5:

		::

			contrail-controller/src/config/utils/provision_control.py
			host@<your_node>:/opt/contrail/utils# python provision_control.py --host_name <host_name> --host_ip <host_ip> --router_asn <asn> --api_server_ip <api_ip> --api_server_port <api_port> --oper add --md5 “juniper” --admin_user admin --admin_password <password>  --admin_tenant_name admin

#. You can also use the web user interface to configure MD5.

			- Connect to the node’s IP address at port 8080 (<node_ip>:8080) and select **Configure->Infrastructure->BGP Routers** . As shown in `Figure 16`_ , a list of BGP peers is displayed.

			.. _Figure 16: 

			*Figure 16* : Edit BGP Router Wndow

			.. figure:: s042480.png


			- For a BGP peer, click on the gear icon on the right hand side of the peer entry. Then click **Edit** . This displays the Edit BGP Router dialog box.


			- Scroll down the window and select **Advanced Options** .


			- Configure the MD5 authentication by selecting **Authentication Mode>MD5** and entering the **Authentication Key** value.

**Related Documentation**

-  `Creating a Virtual Network with Juniper Networks Contrail`_ 

-  `Creating a Virtual Network with OpenStack Contrail`_ 

.. _Creating a Virtual Network with Juniper Networks Contrail: creating-virtual-network-juniper-vnc.html

.. _Creating a Virtual Network with OpenStack Contrail: creating-virtual-network-vnc.html

