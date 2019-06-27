.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

====================================================================
Example: Debugging Connectivity Using Monitoring for Troubleshooting
====================================================================

   -  `Using Monitoring to Debug Connectivity`_ 

Using Monitoring to Debug Connectivity
======================================

This example shows how you can use monitoring to debug connectivity in your Tungsten Fabric system. You can use the demo setup in Tungsten Fabric to use these steps on your own.

#. Navigate to **Monitor -> Networking -> Networks ->**   ``default-domain:demo:vn0`` , **Instance**   ``ed6abd16-250e-4ec5-a382-5cbc458fb0ca`` with **IP address**   ``192.168.0.252`` in the virtual network ``vn0`` ; see `Figure 126`_ 

   .. _Figure 126: 

   *Figure 126* : Navigate to Instance

   .. figure:: s041879.gif



#. Click the instance to view **Traffic Statistics for Instance** . see `Figure 127`_ .

   .. _Figure 127: 

   *Figure 127* : Traffic Statistics for Instance

   .. figure:: s041880.gif



#.  **Instance**   ``d26c0b31-c795-400e-b8be-4d3e6de77dcf`` with **IP address**   ``192.168.0.253`` in the virtual network ``vn16`` . see `Figure 128`_ and 
   
    `Figure 129`_ .

    .. _Figure 128: 

    *Figure 128* : Navigate to Instance

    .. figure:: s041881.gif

    .. _Figure 129: 

    *Figure 129* : Traffic Statistics for Instance

    .. figure:: s041882.gif



#. From **Monitor->Infrastructure->Virtual Routers->**  **a3s18->Interfaces** , we can see that **Instance**  ``ed6abd16-250e-4ec5-a382-5cbc458fb0ca`` is hosted on **Virtual Router**  ``a3s18`` ; see `Figure 130`_ .

   .. _Figure 130: 

   *Figure 130* : Navigate to a3s18 Interfaces

   .. figure:: s041883.gif



#. From **Monitor->Infrastructure->Virtual Routers->**  **a3s19->Interfaces** , we can see that **Instance**  ``d26c0b31-c795-400e-b8be-4d3e6de77dcf`` is hosted on **Virtual Router**  ``a3s19`` ; see `Figure 131`_ .

   .. _Figure 131: 

   *Figure 131* : Navigate to a3s19 Interfaces

   .. figure:: s041884.gif



#.  **Virtual Routers**   ``a3s18`` and ``a3s19`` have the **ACL** entries to allow connectivity between ``default-domain:demo:vn0`` and ``default-domain:demo:vn16`` networks; see `Figure 132`_ and `Figure 133`_ .

    .. _Figure 132: 

    *Figure 132* : ACL Connectivity a3s18

    .. figure:: s041885.gif

    .. _Figure 133: 

    *Figure 133* : ACL Connectivity a3s19

    .. figure:: s041886.gif



#. Next, verify the routes on the control node for routing instances ``default-domain:demo:vn0:vn0`` and ``default-domain:demo:vn16:vn16`` ; see `Figure 134`_ and `Figure 135`_ .

   .. _Figure 134: 

   *Figure 134* : Routes default-domain:demo:vn0:vn0

   .. figure:: s041887.gif

   .. _Figure 135: 

   *Figure 135* : Routes default-domain:demo:vn16:vn16

   .. figure:: s041888.gif



#. We can see that VRF ``default-domain:demo:vn0:vn0`` on Virtual Router ``a3s18`` has the appropriate route and next hop to reach VRF ``default-domain:demo:front-end`` on Virtual Router ``a3s19`` ; see `Figure 136`_ .

   .. _Figure 136: 

   *Figure 136* : Verify Route and Next Hop a3s18

   .. figure:: s041889.gif



#. We can see that VRF ``default-domain:demo:vn16:vn16`` on Virtual Router ``a3s19`` has the appropriate route and next hop to reach VRF ``default-domain:demo:vn0:vn0`` on Virtual Router ``a3s18`` ; see `Figure 137`_ .

   .. _Figure 137: 

   *Figure 137* : Verify Route and Next Hop a3s19

   .. figure:: s041890.gif



#. Finally, flows between instances (IPs ``192.168.0.252`` and ``192.168.16.253`` ) can be verified on Virtual Routers ``a3s18`` and ``a3s19`` ; see `Figure 138`_ and `Figure 139`_ .

   .. _Figure 138: 

   *Figure 138* : Flows for a3s18

   .. figure:: s041891.gif

   .. _Figure 139: 

   *Figure 139* : Flows for a3s19

   .. figure:: s041892.gif


