.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============
Remote Compute
==============



Contrail 5.0 introduces remote compute, a method of managing a Contrail deployment across many small distributed data centers efficiently and cost effectively.

-  `Remote Compute Overview`_ 


-  `Remote Compute Features`_ 


-  `Provisioning a Remote Compute Cluster`_ 




Remote Compute Overview
-----------------------

The remote compute feature is supported starting in Contrail 5.0. The purpose of remote compute is to enable the deployment of Contrail in many small distributed data centers, up to hundreds or even thousands, for telecommunications point-of-presence (PoPs) or central offices (COs). Each small datacenter has only a small number of computes, typically 5-20 in a rack, running a few applications such as video caching, traffic optimization, and virtual Broadband Network Gateway (vBNG). It is not cost effective to deploy a full Contrail controller cluster of nodes of control, configuration, analytics, database, and the like, in each distributed PoP on dedicated servers. Additionally, manually managing hundreds or thousands of clusters is not feasible operationally.



Remote Compute Features
-----------------------

Remote compute is implemented by means of a subcluster that manages compute nodes at remote sites to receive configurations and exchange routes.

The key concepts of Contrail remote compute include:

- Remote compute employs a subcluster to manage remote compute nodes away from the primary datacenter.


- The Contrail control cluster is deployed in large centralized data centers, where it can remotely manage compute nodes in small distributed small data centers.


- A lightweight version of the controller is created, limited to the control node, and the config node, analytics, and analytics database are shared across several control nodes.


- Many lightweight controllers are co-located on a small number of servers to optimize efficiency and cost.


- The control nodes peer with the remote compute nodes by means of XMPP and peer with local gateways by means of MP-eBGP.




Remote Compute Operations
-------------------------

A subcluster object is created for each remote site, with a list of links to local compute nodes that are represented as vrouter objects, and a list of links to local control nodes that are represented as BGP router objects, with an ASN as property.

The subclusters are identified in the provision script. The vrouter and bgp-router provision scripts take each subcluster as an optional argument to link or delink with the subcluster object.

It is recommended to spawn the control nodes of the remote cluster in the primary cluster, and they are IGBP-meshed among themselves within that subcluster. The control nodes BGP-peer with their respective SDN gateway, over which route exchange occurs with the primary control nodes.

Compute nodes in the remote site are provisioned to connect to their respective control nodes to receive configuration and exchange routes. Data communication among workloads between these clusters occurs through the provider backbone and their respective SDN gateways. The compute nodes and the control nodes push analytics data to analytics nodes hosted on the primary cluster.



Subcluster Properties
---------------------

The Contrail UI shows a list of subcluster objects, each with a list of associated vrouters and BGP routers that are local in that remote site and the ASN property.

General properties of subclusters include:

- A subcluster control node never directly peers with another subcluster control node or with primary control nodes.


- A subcluster control node has to be created, and is referred to, in virtual-router and bgp-router objects.


- A subcluster object and the control nodes under it should have the same ASN.


- The ASN cannot be modified in a subcluster object.



.. note:: Multinode service chaining across subclusters is not supported.


Provisioning a Remote Compute Cluster
-------------------------------------

A routing cluster ID object is used to configure the remote compute to build and maintain a correlation between nodes pertaining to the same POP / site / rack.



Web UI for Remote Compute
-------------------------

You can use the Contail Web UI to set up a new remote compute cluster, go to **Configure > Infrastructure > BGP Routers > Edit** .

