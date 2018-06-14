.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================================================
Configuring Traffic Analyzers and Packet Capture for Mirroring
==============================================================

Contrail provides traffic mirroring so you can mirror specified traffic to a traffic analyzer where you can perform deep traffic inspection. Traffic mirroring enables you to designate certain traffic flows to be mirrored to a traffic analyzer, where you can view traffic flows in great detail.

Use **Monitor > Debug > Packet Capture** to configure packets to be captured and “mirrored” to a virtual machine configured as a traffic analyzer. The packet activity can then be inspected for monitoring and troubleshooting purposes. This section demonstrates how to set up packet capture to mirror traffic packets to an analyzer.

-  `Traffic Analyzer Images`_ 


-  `Configuring Traffic Analyzers`_ 


-  `Setting Up Traffic Mirroring Using Monitor > Debug > Packet Capture`_ 


-  `Setting Up Traffic Mirroring Using Configure > Networking > Services`_ 



Traffic Analyzer Images
=======================

Before using the Contrail interface to configure traffic analyzers and packet capture for mirroring, make sure that the following analyzer images are available in the VM image list for your system. The traffic analyzer images are enhanced for viewing details of captured packets in Wireshark. When creating a policy for the traffic analyzer, the traffic analyzer instance should always have the **Mirror to** field selected in the policy, do not select the **Apply Service** field for a traffic analyzer.

-  **analyzer-vm-console-qcow2** —Standard traffic analyzer; should be named **analyzer** in the image list. This type of traffic analyzer is always configured with a single interface, and the interface should be a **Left** interface.


-  **analyzer-vm-console-two-if qcow2** —This type of traffic analyzer has two interfaces, **Left** and **Management** . This traffic analyzer can have any name except the name **analyzer** , which is reserved for the single interface analyzer.



.. note:: The ``analyzer-vm`` images are valid for all versions of Contrail. Download the images from the Contrail 1.0 software download page: https://www.juniper.net/support/downloads/?p=contrail#sw .




Configuring Traffic Analyzers
==============================

In Contrail Controller, you use a two-part configuration to mirror captured packet traffic to a traffic analyzer, where the traffic details can be inspected. The configuration has the following steps:

- Configure analyzer(s) on the host.


- Set up rules for packet capture.


Additionally, there are two ways to configure the packet capture for the analyzers from within the Contrail interface:

- Configure from **Monitor > Debug > Packet Capture** 


- Configure from **Configure > Networking > Services** 



Setting Up Traffic Mirroring Using Monitor > Debug > Packet Capture
===================================================================

The following are the steps needed to set up packet capture in order to “mirror” the traffic to an analyzer VM for the purpose of reviewing various aspects of packet traffic moving through the system.


#. Select **Monitor > Debug > Packet Capture** . The **Packet Capture** screen appears; see `Figure 137`_ .

   .. _Figure 137: 

   *Figure 137* : Packet Capture

   .. figure:: s041617.gif



#. Click **Create** to add an analyzer; see `Figure 138`_ .

   .. _Figure 138: 

   *Figure 138* : Create Analyzer

   .. figure:: s041616.gif



#. In the **Analyzer Name** field, enter a name for the analyzer and in the **Virtual Network** field, select **Automatic** or select a specific virtual network from the drop-down list of available networks; click **Save** when finished.



#. To create rules for the analyzer, in the lower portion of the **Create Analyzer** screen, click the **+** button to add a rule.

   The **Analyzer Rules** fields appear; see `Figure 139`_ .

   .. _Figure 139: 

   *Figure 139* : Analyzer Rules

   .. figure:: s041618.gif



#. Select the rules to apply to determine which packets should be “mirrored”—sent to the analyzer for monitoring.

   See `Table 31`_ for guidelines for completing the rule fields.

   

    .. _Table 31: 


   *Table 31* : Analyzer Rule Fields

   +-----------------------------------+-----------------------------------+
   | Field                             | Description                       |
   +===================================+===================================+
   | **IP Protocol**                   | Select from a list to define from |
   |                                   | which protocol packets are to be  |
   |                                   | captured:                         |
   |                                   |                                   |
   |                                   | -  ANY                            |
   |                                   | -  TCP                            |
   |                                   | -  UDP                            |
   |                                   | -  ICMP                           |
   +-----------------------------------+-----------------------------------+
   | **Source Network**                | Select from a list the source     |
   |                                   | network from which packets are to |
   |                                   | be captured:                      |
   |                                   |                                   |
   |                                   | -  any                            |
   |                                   | -  local                          |
   |                                   | -  *domain:network 1*             |
   |                                   | -  *domain:network 2*             |
   |                                   | -  *domain:network .....*         |
   +-----------------------------------+-----------------------------------+
   | **Source Ports**                  | If you want to capture only those |
   |                                   | packets that originate from a     |
   |                                   | specific port number, enter the   |
   |                                   | port number.                      |
   +-----------------------------------+-----------------------------------+
   | **Direction**                     | Select the direction of flow for  |
   |                                   | the packets to be captured:       |
   |                                   |                                   |
   |                                   | -  Bidirectional                  |
   |                                   | -  Unidirectional                 |
   +-----------------------------------+-----------------------------------+
   | **Destination Network**           | Select from a list the            |
   |                                   | destination network for the       |
   |                                   | packets to be captured:           |
   |                                   |                                   |
   |                                   | -  any                            |
   |                                   | -  local                          |
   |                                   | -  *domain:network 1*             |
   |                                   | -  *domain:network 2*             |
   |                                   | -  *domain:network .....*         |
   +-----------------------------------+-----------------------------------+
   | **Destination Ports**             | If you want to capture only those |
   |                                   | packets that are destined to a    |
   |                                   | specific port number, enter the   |
   |                                   | port number.                      |
   +-----------------------------------+-----------------------------------+
   | Cancel, Save                      | When finished, click **Save** to  |
   |                                   | commit your selections, or click  |
   |                                   | **Cancel** to clear the entries   |
   |                                   | and start over.                   |
   +-----------------------------------+-----------------------------------+



#. To associate virtual networks with the analyzer, click the **Associate Networks** field in the center portion of the screen. Select from a drop-down list of available networks the networks to associate with this analyzer; see `Figure 140`_ .

   .. _Figure 140: 

   *Figure 140* : Create Analyzer Associate Networks

   .. figure:: s041614.gif


   .. note:: If there is already a network policy attached to the virtual network selected, any conflicting rules configured for the analyzer will not take effect.





#. View the analyzer activity from **Monitor > Debug > Packet Capture** . For the selected analyzer, click in the **Action** column and select **View Analyzer** ; see `Figure 141`_ .

   .. _Figure 141: 

   *Figure 141* : Launch Analyzer VM

   .. figure:: s041546.gif



#. The Wireshark **Packet Capture Display** appears; see `Figure 142`_ .

   .. _Figure 142: 

   *Figure 142* : Packet Capture Display

   .. figure:: s041615.gif



Setting Up Traffic Mirroring Using Configure > Networking > Services
====================================================================

You can set up packet capture for mirroring to an analyzer within a service chain utilizing more than one interface by starting with a service template. The following procedure provides the steps needed.


#. Access **Configure > Services > Service Templates** .

   The **Service Templates** screen appears; see `Figure 143`_ .

   .. _Figure 143: 

   *Figure 143* : Service Templates

   .. figure:: s041612.gif



#. To create a new service template, click the **+** icon.

   The **Create** window appears. Select the Service Template tab; see `Figure 144`_ .

   .. _Figure 144: 

   *Figure 144* : Create Service Template

   .. figure:: s041613.gif



#. Complete the fields by using the guidelines in `Table 32`_ .

   .. _Table 32: 


   *Table 32* : Create Service Template Fields

   +-----------------------------------+-----------------------------------+
   | Field                             | Description                       |
   +===================================+===================================+
   | **Name**                          | Enter a descriptive text name for |
   |                                   | this service template.            |
   +-----------------------------------+-----------------------------------+
   | **Version**                       | Select **v2** from the drop-down  |
   |                                   | list to indicate that this        |
   |                                   | service template is based on      |
   |                                   | templates version 2, valid for    |
   |                                   | Contrail 3.0 and later.           |
   +-----------------------------------+-----------------------------------+
   | **Virtualization Type**           | Select **Virtual Machine** from   |
   |                                   | the drop-down list to indicate    |
   |                                   | the virtualization type for       |
   |                                   | mirroring for this template.      |
   +-----------------------------------+-----------------------------------+
   | **Service Mode**                  | Select **Transparent** from the   |
   |                                   | drop-down list to indicate that   |
   |                                   | this service template is for      |
   |                                   | transparent mirroring.            |
   +-----------------------------------+-----------------------------------+
   | **Service Type**                  | Select **Analyzer** from the      |
   |                                   | drop-down list to indicate that   |
   |                                   | this service template is for a    |
   |                                   | traffic analyzer.                 |
   +-----------------------------------+-----------------------------------+
   | **Interface(s)**                  | From the drop-down list, click    |
   |                                   | the check boxes to indicate which |
   |                                   | interface types are used for this |
   |                                   | analyzer service template:        |
   |                                   |                                   |
   |                                   | -  Left                           |
   |                                   | -  Right                          |
   |                                   | -  Management                     |
   +-----------------------------------+-----------------------------------+
   | **Save**                          | When finished, click **OK** to    |
   |                                   | commit the changes                |
   +-----------------------------------+-----------------------------------+
   | **Cancel**                        | Click **Cancel** to clear the     |
   |                                   | fields and start over.            |
   +-----------------------------------+-----------------------------------+




#. Create a service instance by clicking the **Service Instances** link and clicking the **+** icon.

   The **Create** window appears; make sure the Service Instance tab is selected. See `Figure 145`_ .

   .. _Figure 145: 

   *Figure 145* : Create Service Instances

   .. figure:: s041858.gif



#. Complete the fields by using the guidelines in `Table 33`_ .

   .. _Table 33: 


   *Table 33* : Create Service Instances Fields

   +-----------------------------------+-----------------------------------+
   | Field                             | Description                       |
   +===================================+===================================+
   | **Name**                          | Enter a text name for this        |
   |                                   | service instance.                 |
   +-----------------------------------+-----------------------------------+
   | **Service Template**              | Select from a drop-down list of   |
   |                                   | available service templates the   |
   |                                   | template to use for this service  |
   |                                   | instance,                         |
   |                                   | analyzer-service-template in this |
   |                                   | example.                          |
   +-----------------------------------+-----------------------------------+
   | **Interface Type**                | Each interface configured in the  |
   |                                   | service template for this         |
   |                                   | instance appears in a list.       |
   +-----------------------------------+-----------------------------------+
   | **Virtual Network**               | Select from a drop-down list of   |
   |                                   | available virtual networks the    |
   |                                   | network for each interface that   |
   |                                   | is configured for the instance.   |
   +-----------------------------------+-----------------------------------+
   | **Save**                          | Click **Save** to commit your     |
   |                                   | changes.                          |
   +-----------------------------------+-----------------------------------+
   | **Cancel**                        | Click **Cancel** to clear your    |
   |                                   | changes and start over.           |
   +-----------------------------------+-----------------------------------+





#. To create a network policy rule for this service instance, click **Configure > Networking > Policies** . The **Policies** window appears. Click the **+** icon to get to the **Create** window; see `Figure 146`_ .

   .. _Figure 146: 

   *Figure 146* : Create Policy

   .. figure:: s041859.gif


#. Enter a name for the policy, then click the + icon in the lower portion of the screen to configure rules for the policy, see `Figure 147`_ .

   .. _Figure 147: 

   *Figure 147* : Create Policy Rules

   .. figure:: s041833.gif



#. To add policy rules, complete the fields, using the guidelines in `Table 34`_ .


   .. note:: When there is a network policy attached to the virtual network, any conflicting rules configured for the analyzer will not take effect.



   .. _Table 34: 


   *Table 34* : Add Rule Fields

   +-----------------------------------+-----------------------------------+
   | Field                             | Description                       |
   +===================================+===================================+
   | **Action**                        | Select PASS or DENY as the rule   |
   |                                   | action.                           |
   +-----------------------------------+-----------------------------------+
   | **Protocol**                      | Select the protocol for the       |
   |                                   | policy rule, or select ANY.       |
   +-----------------------------------+-----------------------------------+
   | **Source**                        | Select from multiple drop-down    |
   |                                   | lists the source for this rule,   |
   |                                   | including options under CIDR,     |
   |                                   | Network, Policy, or Security      |
   |                                   | Group.                            |
   +-----------------------------------+-----------------------------------+
   | **Ports**                         | Select from a drop-down list the  |
   |                                   | source ports for the rule.        |
   +-----------------------------------+-----------------------------------+
   | **Direction**                     | Select the direction of flow for  |
   |                                   | the packets to be captured:       |
   |                                   |                                   |
   |                                   | -  <> (bidirectional)             |
   |                                   | -  > (unidirectional)             |
   +-----------------------------------+-----------------------------------+
   | **Destination**                   | Select from multiple drop-down    |
   |                                   | lists the destination for this    |
   |                                   | rule, including options under     |
   |                                   | CIDR, Network, Policy, or         |
   |                                   | Security Group.                   |
   +-----------------------------------+-----------------------------------+
   | **Ports**                         | Select from a list the            |
   |                                   | destination ports for the packets |
   |                                   | to be captured.                   |
   +-----------------------------------+-----------------------------------+
   | **check boxes**                   | Check any box that applies to     |
   |                                   | this rule: Log, Services, Mirror, |
   |                                   | QoS.                              |
   +-----------------------------------+-----------------------------------+
   | **Save**                          | Click **Save** to commit your     |
   |                                   | changes.                          |
   +-----------------------------------+-----------------------------------+
   | **Cancel**                        | Click **Cancel** to clear your    |
   |                                   | changes and start over.           |
   +-----------------------------------+-----------------------------------+



#. When finished, click **Save** .



#. To verify packet capture, at **Configure > Services > Service Instances** , select the analyzer service instance and click **View Console** .

   The packet capture displays; see `Figure 148`_ . The analyzer service VM launches the Contrail-enhanced Wireshark as it starts and captures the mirrored packets destined to this service.

   .. _Figure 148: 

   *Figure 148* : Service Instances View Console

   .. figure:: s041869.gif


**Related Documentation**

-  `Configuring Interface Monitoring and Mirroring`_ 

-  `Mirroring Enhancements`_ 

-  `Analyzer Service Virtual Machine`_ 

-  `Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring)`_ 

.. _Configuring Interface Monitoring and Mirroring: interface-monitor-mirror-vnc.html

.. _Mirroring Enhancements: mirroring-enhancements-vnc.html

.. _Analyzer Service Virtual Machine: analyzer-vm.html

.. _Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring): nic-assisted-mirroring.html


.. _https://www.juniper.net/support/downloads/?p=contrail#sw: https://www.juniper.net/support/downloads/?p=contrail#sw
