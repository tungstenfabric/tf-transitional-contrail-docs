.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================
Quality of Service in Contrail
==============================

-  `Overview: Quality of Service`_ 


-  `Contrail QoS Model`_ 


-  `QoS Configuration Parameters for Provisioning`_ 


-  `Queuing Implementation`_ 


-  `Contrail QoS Configuration Objects`_ 


-  `Example: Mapping Traffic to Forwarding Classes`_ 


-  `QoS Configuration Object Marking on the Packet`_ 


-  `Queuing`_ 


-  `Queue Selection in Datapath`_ 


-  `Parameters for QoS Scheduling Configuration`_ 




Overview: Quality of Service
----------------------------

Quality of service (QoS) in networking provides the ability to control reliability, bandwidth, latency, and other traffic management features. Network traffic can be marked with QoS bits (DSCP, 802.1p, and MPLS EXP) that intermediate network switches and routers can use to provide service guarantees.



Contrail QoS Model
------------------

The Contrail QoS model has the following features:

- All packet forwarding devices, such as vRouter and the gateway, combine to form a system.


- Interfaces to the system are the ports from which the system sends and receives packets, such as tap interfaces and physical ports.


- Fabric interfaces are where the overlay traffic is tunneled.


- QoS is applied at the ingress to the system, for example, upon traffic from the interfaces to the fabric.


- At egress, packets are stripped of their tunnel headers and sent to interface queues, based on the forwarding class. No marking from the outer packet to the inner packet is considered at this time.




Features of Fabric Interfaces
-----------------------------

Fabric interfaces, unlike other interfaces, are always shared. Therefore, fabric interfaces are common property. Consequently, traffic classes and QoS marking on the fabric must be controlled by the system administrator. The administrator might choose to provision different classes of service on the fabric.

In Contrail, classes of service are determined by both of the following:

- Queueing on the fabric interface, including queues, scheduling of queues, and drop policies, and


- forwarding class, a method of marking that controls how packets are sent to the fabric, including marking and identifying which queue to use.


Tenants can define which forwarding class their traffic can use, deciding which packets use which forwarding class. The Contrail QoS configuration object has a mapping table, mapping the incoming DSCP or 802.1p value to the forwarding class mapping.

The QoS configuration can also be applied to a virtual network, an interface, or a network policy.



QoS Configuration Parameters for Provisioning
---------------------------------------------

-  `Testbed.py Parameters`_ 




Testbed.py Parameters
---------------------

 ``Testbed.py`` can be used for provisioning Contrail through Releases 3.x.x. Starting with Contrail 4.0, ``testbed.py`` can only be used if you are provsioning with SM-Lite. Use parameters in this section if you are using ``testbed.py`` for provisioning.
For QoS, the hardware queues (NIC queues) are mapped to logical queues in the agent, using the following keys:
   - hardware_q_id—Identifier for the hardware queue.


- logical_queue— Defines the logical queues to map to each hardware queue.


- default—Defines the default hardware queue for QoS when set to True.


Options to define a default hardware queue:


#. Set the queue as default, without any logical queue mapping.

    ``{'hardware_q_id': '1', 'default': 'True'}`` 



#. Set the hardware queue as default with logical queue mapping.
    ``{'hardware_q_id': '6', 'logical_queue':['17-20'], 'default': 'True'}`` 

   ::

      env.qos = {host4: [ {'hardware_q_id': '3', 'logical_queue':['1', '6-10', '12-15']},
              {'hardware_q_id': '5', 'logical_queue':['2']},
              {'hardware_q_id': '8', 'logical_queue':['3-5']},
              {'hardware_q_id': '1', 'default': 'True'}],
     host5: [ {'hardware_q_id': '2', 'logical_queue':['1', '3-8', '10-15']},
              {'hardware_q_id': '6', 'logical_queue':['17-20'], 'default': 'True'}]
    }



The following are the keys for defining QoS priority groups.
- priority_id—Priority group for QoS.


- scheduling—Defines the scheduling algorithm used for the priority group, strict or roundrobin (rr).


- bandwidth—Total hardware queue bandwidth used by priority group.

Bandwidth cannot be specified if strict scheduling is used for priority group, so set it to 0.



Example: QoS Priority Group
---------------------------


::

 env.qos_niantic = {host4:[
       { 'priority_id': '1', 'scheduling': 'strict', 'bandwidth': '0'},
       { 'priority_id': '2', 'scheduling': 'rr', 'bandwidth': '20'},
       { 'priority_id': '3', 'scheduling': 'rr', 'bandwidth': '10'}],
           host5:[
       { 'priority_id': '1', 'scheduling': 'strict', 'bandwidth': '0'},
       { 'priority_id': '1', 'scheduling': 'rr', 'bandwidth': '30'}]
                }




Queuing Implementation
----------------------

Starting with Contrail 3.2, queuing is added. The vRouter provides the infrastructure to use queues supplied by the network interface, a method that is also called hardware queueing. Network interface cards (NICs) that implement hardware queueing have their own set of scheduling algorithms associated with the queues. The Contrail implementation is designed to work with most NICs, however, the method is tested only on an Intel-based 10G NIC, also called Niantic.



QoS Features by Release
-----------------------

QoS features are introduced in the following Contrail releases:

- 3.1—QoS configuration and forwarding classes


- 3.2—queuing


- Not planned—egress marking and queuing




Contrail QoS Configuration Objects
----------------------------------

Contrail QoS configuration objects include the:

- forwarding class


- QoS configuration object ( ``qos-config`` )


The forwarding class object specifies parameters for marking and queuing, including:

- The DSCP, 802.1p, and MPLS EXP values to be written on packets.


- The queue index to be used for the packet.


The QoS configuration object specifies a mapping from DSCP, 802.1p, and MPLS EXP values to the corresponding forwarding class.

The QoS configuration has an option to specify the default forwarding class ID to use to select the forwarding class for all unspecified DSCP, 802.1p, and MPLS EXP values.

If the default forwarding class ID is not specified by the user, it defaults to the forwarding class with ID 0.

Processing of QoS marked packets to look up the corresponding forwarding class to be applied works as follows:

- For an IP packet, the DSCP map is used .


- For a Layer 2 packet, the 802.1p map is used.


- For an MPLS-tunneled packet with MPLS EXP values specified, the EXP bit value is used with the MPLS EXP map.


- If the QoS configuration is untrusted, only the default forwarding class is specified, and all incoming values of the DSCP, 802.1p, and EXP bits in the packet are mapped to the same default forwarding class.


`Figure 113`_ shows the processing of QoS packets.

.. _Figure 113: 

*Figure 113* : Processing of QoS Packets

.. figure:: s018750.png

A virtual machine interface, virtual network, and network policy can refer to the QoS configuration object. The QoS configuration object can be specified on the vhost so that underlay traffic can also be subjected to marking and queuing. See `Figure 114`_ .

.. _Figure 114: 

*Figure 114* : Referring to the QoS Object

.. figure:: s018751.png



Example: Mapping Traffic to Forwarding Classes
----------------------------------------------

This example shows how traffic forwarding classes are defined and how the QoS configuration object is defined to map the QoS bits to forwarding classes.

`Table 27`_ shows two forwarding class objects defined. FC1 marks the traffic with high priority values and queues it to Queue 0. FC2 marks the traffic as best effort and queues the traffic to Queue 1.

.. _Table 27: 


*Table 27* : Forwarding Class Mapping

+------+----+------+--------+----------+-------+
| Name | ID | DSCP | 802.1p | MPLS EXP | Queue |
+======+====+======+========+==========+=======+
| FC1  | 1  | 10   | 7      | 7        | 0     |
+------+----+------+--------+----------+-------+
| FC2  | 2  | 38   | 0      | 0        | 1     |
+------+----+------+--------+----------+-------+

In `Table 28`_ , the QoS configuration object DSCP values of 10, 18, and 26 are mapped to a forwarding class with ID 1, which is forwarding class FC1. All other IP packets are mapped to the forwarding class with ID 2, which is FC2. All traffic with an 802.1p value of 6 or 7 are mapped to forwarding class FC1, and the remaining traffic is mapped to FC2.

.. _Table 28: 


*Table 28* : QoS Configuration Object Mapping

+-----------+-----------+-----------+-----------+-----------+-----------+
| DSCP      | Forwardin | 802.1p    | Forwardin | MPLS EXP  | Forwardin |
|           | g         |           | g         |           | g         |
|           | Class ID  |           | Class ID  |           | Class ID  |
+===========+===========+===========+===========+===========+===========+
| 10        | 1         | 6         | 1         | 5         | 1         |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 18        | 1         | 7         | 1         | 7         | 1         |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 26        | 1         | \*        | 2         | \*        | 1         |
+-----------+-----------+-----------+-----------+-----------+-----------+
| \*        | 2         |           |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+



QoS Configuration Object Marking on the Packet
----------------------------------------------

The following describes how QoS configuration object marking is handled in various circumstances.



Traffic Originated by a Virtual Machine Interface
-------------------------------------------------

- If a VM interface sends an IP packet to another VM in a remote compute node, the DSCP value in the IP header is used to look into the qos-config table, and the tunnel header is marked with DSCP, 802.1p, and MPLS EXP bits as specified by the forwarding class.


- If a VM sends a Layer 2 non-IP packet with an 802.1p value, the 802.1p value is used to look into the qos-config table, and the corresponding forwarding class DSCP, 802.1p, and MPLS EXP value is written to the tunnel header.


- If a VM sends an IP packet to a VM in the same compute node, the DSCP value in the IP header is matched in the qos-config table, and the corresponding forwarding class is used to overwrite the IP header with new DSCP and 802.1p values.




Traffic Destined to a Virtual Machine Interface
-----------------------------------------------

For traffic destined to a VMI, if a tunneled packet is received, the tunnel headers are stripped off and the packet is sent to the interface. No marking is done from the outer packet to inner packet.



Traffic from a vhost Interface
------------------------------

The QoS configuration can be applied on IP traffic coming from a vhost interface. The DSCP value in the packet is used to look into the qos-config object specified on the vhost, and the corresponding forwarding class DSCP and 802.1p values are overwritten on the packet.



Traffic from fabric interface
-----------------------------

The QoS configuration can be applied while receiving the packet on an Ethernet interface of a compute node, and the corresponding forwarding class DSCP and 802.1p values are overwritten on the packet.



QoS Configuration Priority by Level
-----------------------------------

The QoS configuration can be specified at different levels.

The levels that can be configured with QoS and their order of priority:

- in policy


- on ``virtual-network`` 


- on ``virtual-machine-interface`` 




Queuing
-------

Contrail Release 3.2 adds QoS support for queuing.

This section provides an overview of the queuing features available starting with Contrail 3.2.

For more details about any of these topics, see: https://github.com/Juniper/contrail-controller/wiki/QoS .

The queue to which a packet is sent is specified by the forwarding class.



Queue Selection in Datapath
---------------------------

In vRouter, in the data path, the forwarding class number specifies the actual physical hardware queue to which the packet needs to be sent, not to a logical selection as in other parts of Contrail. There is a mapping table in the vRouter configuration file, to translate the physical queue number from the logical queue number.



Hardware Queueing in Linux kernel based vRouter
-------------------------------------------------

If Xmit-Packet-Steering (XPS) is enabled, the kernel chooses the queue, from those available in a list of queues. If the kernel selects the queue, packets will not be sent to the vRouter-specified queue.

To disable this mapping:

- have a kernel without CONFIG_XPS option


- write zeros to the mapping file in /sys/class/net//queues/tx-X/xps_cpus .


When this mapping is disabled, the kernel will send packets to the specific hardware queue.

To verify:

See individual queue statistics in the output of 'ethtool -S ' command.



Parameters for QoS Scheduling Configuration
-------------------------------------------

The following shows sample scheduling configuration for hardware queues on the compute node.
The priority group ID and the corresponding scheduling algorithm and bandwidth to be used by the priority group can be configured.
Possible values for the scheduling algorithm include:

- strict


- rr (round-robin)


When round-robin scheduling is used, the percentage of total hardware queue bandwidth that can be used by the priority group is specified in the bandwidth parameter.
The following configuration and provisioning is applicable only for compute nodes running Niantic NICs and running kernel based vrouter.

::

 qos_niantic =  {
     ‘compute1': [ 
                       { 'priority_id': '1', 'scheduling': 'strict', 'bandwidth': '0'},
                       { 'priority_id': '2', 'scheduling': 'rr', 'bandwidth': '20'},
                       { 'priority_id': '3', 'scheduling': 'rr', 'bandwidth': '10’}
     ],
     ‘compute2' :[ 
                       { 'priority_id': '1', 'scheduling': 'strict', 'bandwidth': '0'},
                       { 'priority_id': '1', 'scheduling': 'rr', 'bandwidth': '30’}
      ]
 }


**Related Documentation**

-  `Configuring Network QoS Parameters`_ 

-  https://github.com/Juniper/contrail-controller/wiki/QoS . 

.. _Configuring Network QoS Parameters: network-qos-configuring.html


.. _https://github.com/Juniper/contrail-controller/wiki/QoS: https://github.com/Juniper/contrail-controller/wiki/QoS

.. _https://github.com/Juniper/contrail-controller/wiki/QoS .: https://github.com/Juniper/contrail-controller/wiki/QoS .
