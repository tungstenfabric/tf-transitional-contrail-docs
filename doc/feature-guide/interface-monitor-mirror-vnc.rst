.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================================
Configuring Interface Monitoring and Mirroring
==============================================

Contrail supports user monitoring of traffic on any guest virtual machine interface when using the Juniper Contrail user interface.

When interface monitoring (packet capture) is selected, a default analyzer is created and all traffic from the selected interface is mirrored and sent to the default analyzer. If a mirroring instance is already launched, the traffic will be redirected to the selected instance. The interface traffic is only mirrored during the time that the monitor packet capture interface is in use. When the capture screen is closed, interface mirroring stops.

To configure interface mirroring:

- Select **Monitor > Infrastructure > Virtual Routers** , then select the vRouter that has the interface to mirror.


- In the list of attributes for the vRouter, select Interfaces; see `Figure 149`_ .

.. _Figure 149: 

*Figure 149* : Individual vRouter

.. figure:: s041839.gif

A list of interfaces for that vRouter appears.


- For the interface to mirror, click the Action icon in the last column and select the option Packet Capture; see `Figure 150`_ .

.. _Figure 150: 

*Figure 150* : Interfaces

.. figure:: s041856.gif

The mirror packet capture starts and displays at this screen.

The mirror packet capture stops when you exit this screen.


**Related Documentation**

-  `Configuring Traffic Analyzers and Packet Capture for Mirroring`_ 

-  `Mirroring Enhancements`_ 

-  `Analyzer Service Virtual Machine`_ 

-  `Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring)`_ 

.. _Configuring Traffic Analyzers and Packet Capture for Mirroring: configure-traffic-analyzer-vnc.html

.. _Mirroring Enhancements: mirroring-enhancements-vnc.html

.. _Analyzer Service Virtual Machine: analyzer-vm.html

.. _Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring): nic-assisted-mirroring.html

