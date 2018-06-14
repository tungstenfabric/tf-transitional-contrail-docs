.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===============================================================
Example: Creating an In-Network or In-Network-NAT Service Chain
===============================================================

This section provides an example of creating an ``in-network`` service chain and an ``in-network-nat`` service chain using the Juniper Networks Contrail user interface. This service chain example also shows scaling of service instances.

-  `Creating an In-Network or In-Network-NAT Service Chain`_ 




Creating an In-Network or In-Network-NAT Service Chain
------------------------------------------------------

To create an **in-network** or **in-network-nat** service chain:


#. Create a left and a right virtual network. Select **Configure > Networking > Networks** and create **left_vn** and **right_vn** ; see `Figure 96`_ .

   .. _Figure 96: 

   *Figure 96* : Create Networks

   .. figure:: s041865.gif



#. Configure a service template for an in-network service template for NAT. Navigate to **Configure > Services > Service Templates** and click the **Create** button on **Service Templates** . The **Add Service Template** window appears; see `Figure 97`_ .

   .. _Figure 97: 

    *Figure 97* : Add Service Template

   .. figure:: s041902.gif

   .. _Table 23: 


   *Table 23* : Add Service Template Fields

   +-----------------------------------+-----------------------------------+
   | Field                             | Description                       |
   +===================================+===================================+
   | **Name**                          | Enter a name for the service      |
   |                                   | template.                         |
   +-----------------------------------+-----------------------------------+
   | **Service Mode**                  | Select the service mode:          |
   |                                   | **In-Network** (for firewall      |
   |                                   | service), **In-Network-NAT** (for |
   |                                   | NAT service), or **Transparent**. |
   +-----------------------------------+-----------------------------------+
   | **Service Scaling**               | If you will be using multiple     |
   |                                   | virtual machines for a single     |
   |                                   | service instance to scale out the |
   |                                   | service, select the **Service     |
   |                                   | Scaling** check box. When scaling |
   |                                   | is selected, you can choose to    |
   |                                   | use the same IP address for a     |
   |                                   | particular interface on each      |
   |                                   | virtual machine interface or to   |
   |                                   | allocate new addresses for each   |
   |                                   | virtual machine. For a NAT        |
   |                                   | service, the left (inner)         |
   |                                   | interface should have the same IP |
   |                                   | address, and the right (outer)    |
   |                                   | interface should have a different |
   |                                   | IP address.                       |
   +-----------------------------------+-----------------------------------+
   | **Image Name**                    | Select from a list of available   |
   |                                   | images the image for the service. |
   |                                   |                                   |
   |                                   | **Note:** Only images that have   |
   |                                   | been tagged as public in Glance   |
   |                                   | will appear in the drop-down      |
   |                                   | list.                             |
   +-----------------------------------+-----------------------------------+
   | **Interface Types**               | Select the interface type or      |
   |                                   | types for this service:           |
   |                                   |                                   |
   |                                   | -  For firewall or NAT services,  |
   |                                   |    both **Left Interface** and    |
   |                                   |    **Right Interface** are        |
   |                                   |    required.                      |
   |                                   |                                   |
   |                                   | -  For an analyzer service, only  |
   |                                   |    a **Left Interface** is        |
   |                                   |    required.                      |
   |                                   |                                   |
   |                                   | -  For Juniper Networks virtual   |
   |                                   |    images, **Management           |
   |                                   |    Interface** is also required,  |
   |                                   |    in addition to any left or     |
   |                                   |    right requirement.             |
   +-----------------------------------+-----------------------------------+



#. On **Add Service Template** , complete the following for the in-network service template:

   -  **Name** : nat-template


   -  **Service Mode** : In-Network


   -  **Service Scaling** : Select from Advanced


   -  **Image Name** : nat-service


   -  **Interface Types** : Select Left Interface and Right Interface. For Juniper Networks virtual images, select Management Interface as the first interface.


   - The Left Interface will be automatically marked for sharing the same IP address




#. If multiple instances are to be launched for a particular service instance, select the **Service Scaling** check box, which enables the **Shared IP** feature. `Figure 98`_ shows the **Left** interface selected, with the **Shared IP** check box selected, so the left interface will share the IP address.


  .. note:: The **Shared IP** for **Service Scaling** is an internal infrastructure feature used only for service scaling, it cannot be used for other features.



  .. _Figure 98: 

  *Figure 98* : Add Service Template Shared IP

  .. figure:: s041903.gif



#. Click **Save** .

   The service template is created and appears on the **Service Templates** screen, see `Figure 99`_ .

   .. _Figure 99: 

   *Figure 99* : Service Templates

   .. figure:: s041900.gif



#. Create the service instance. Navigate to **Configure > Services > Service Instances** , and click **Create** , then select the template to use and select the corresponding left, right, or management networks; see `Figure 100`_ .

   .. _Figure 100: 

   *Figure 100* : Create Service Instances

   .. figure:: s041867.gif

   .. _Table 24: 


   *Table 24* : Create Service Instances Fields

   +-----------------------------------+-----------------------------------+
   | Field                             | Description                       |
   +===================================+===================================+
   | **Instance Name**                 | Enter a name for the service      |
   |                                   | instance.                         |
   +-----------------------------------+-----------------------------------+
   | **Services Template**             | Select from a list of available   |
   |                                   | service templates the service     |
   |                                   | template to use for this          |
   |                                   | instance.                         |
   +-----------------------------------+-----------------------------------+
   | **Number of Instances**           | If scaling is enabled, enter a    |
   |                                   | value in the **Number of          |
   |                                   | Instances** field to define the   |
   |                                   | number of instances of service    |
   |                                   | virtual machines to launch.       |
   +-----------------------------------+-----------------------------------+



#. If static routes are enabled for specific interfaces, open the **Static Routes** field below each enabled interface and enter the static route address details; see `Figure 101`_ .

   .. _Figure 101: 

   *Figure 101* : Create Service Instances

   .. figure:: s041868.gif



#. The console for the service instances can be viewed. At **Configure > Services > Service Instances** , click the arrow next to the name of the service instance to reveal the details panel for that instance, then click **View Console** to see the console details; see `Figure 102`_ and `Figure 103`_ .

   .. _Figure 102: 

   *Figure 102* : Service Instance Details

   .. figure:: s041869.gif

   .. _Figure 103: 

   *Figure 103* : Service Instance Console

   .. figure:: s041919.gif



#. Configure the network policy. Navigate to **Configure > Networking > Policies** .

   - Name the policy and associate it with the networks created earlier: **left_vn** and **right_vn** .


   - Set source network as **left_vn** and destination network as **right_vn** .


   - Select **Apply Service** and select the service ( **nat-ecmp** ).


   .. _Figure 104: 

   *Figure 104* : Create Policy

   .. figure:: s041870.gif



#. Associate the policy with both the **left_vn** and the **right_vn** . Navigate to **Configure > Networking > Network** .

   - On the right side of **left_vn** , click the gear icon to enable **Edit Network** .


   - In the **Edit Network** dialog box for **left_vn** , select **nat-policy** in the **Network Policy(s)** field.


   - Repeat the same process for the **right_vn** .


   .. _Figure 105: 

   *Figure 105* : Edit Network

   .. figure:: s041920.gif



#. Launch virtual machines (from OpenStack) and test the traffic through the service chain by doing the following:

   - Navigate to **Configure > Networking > Policies** .


   - Launch **left_vm** in virtual network **left_vn** .


   - Launch **right_vm** in virtual network **right_vn** .


   - Ping from **left_vm** to **right_vm** IP address **(2.2.2.252** in `Figure 106`_ ).


   - A **TCPDUMP** on the **right_vm** should show that packets are NAT-enabled and have the source IP set to **2.2.2.253** .


   .. _Figure 106: 

   *Figure 106* : Launch Instances

   .. figure:: s041871.gif


**Related Documentation**

-  `Service Chaining`_ 

-  `Example\:\ Creating a Transparent Service Chain`_ 

-  `ECMP Load Balancing in the Service Chain`_ 

.. _Service Chaining: service-chaining-vnc.html

.. _Example\:\ Creating a Transparent Service Chain: service-chaining-transparent.html

.. _ECMP Load Balancing in the Service Chain: load-balancing-vnc.html

