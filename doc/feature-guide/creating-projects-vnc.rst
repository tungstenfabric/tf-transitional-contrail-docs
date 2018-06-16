.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==================================================================
Creating Projects in OpenStack for Configuring Tenants in Contrail
==================================================================

In Contrail, a tenant configuration is called a project. A project is created for each set of virtual machines (VMs) and virtual networks (VNs) that are configured as a discrete entity for the tenant.

Projects are created, managed, and edited at the OpenStack **Projects** page.


#. Click the **Admin** tab on the OpenStack dashboard, then click the **Projects** link to access the **Projects** page; see `Figure 50`_ 

   .. _Figure 50: 

   *Figure 50* : OpenStack Projects

   .. figure:: s041521.gif



#. In the upper right, click the **Create Project** button to access the **Add Project** window; see `Figure 51`_ .

   .. _Figure 51: 

   *Figure 51* : Add Project

   .. figure:: s041522.gif



#. In the **Add Project** window, on the **Project Info** tab, enter a **Name** and a **Description** for the new project, and select the **Enabled** check box to activate this project.



#. In the **Add Project** window, select the **Project Members** tab, and assign users to this project. Designate each user as **admin** or as **Member** .

   As a general rule, one person should be a super user in the **admin** role for all projects and a user with a **Member** role should be used for general configuration purposes.



#. Click **Finish** to create the project.


Refer to OpenStack documentation for more information about creating and managing projects.

**Related Documentation**

-  `Creating a Virtual Network with Juniper Networks Contrail`_ 

-  `Creating a Virtual Network with OpenStack Contrail`_ 

-  `OpenStack documentation`_  

.. _Creating a Virtual Network with Juniper Networks Contrail: creating-virtual-network-juniper-vnc.html

.. _Creating a Virtual Network with OpenStack Contrail: creating-virtual-network-vnc.html


.. _OpenStack documentation: http://docs.openstack.org/
