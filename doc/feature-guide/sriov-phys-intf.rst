.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================================
SR-IOV VF as the Physical Interface of vRouter
==============================================

Starting with Contrail 3.0, support is provided for single-root I/O virtualization (SR-IOV) virtual functions used as the physical router for vRouter.

SR-IOV allows a network interface to separate the access to its resources across multiple PCI Express functions. The functions can be physical or virtual.

The Contrail vRouter can use an SR-IOV virtual function as its physical interface. One virtual function on a network interface can be used by vRouter, while the remaining virtual functions can be used by virtual machines on the same compute node. It is also possible to create a VLAN interface on a virtual function, and use that as the physical interface of the vRouter.

Alternatively, virtual functions from two different interfaces can be bonded together, and that bonded interface can be used as the physical interface of the vRouter. It is also possible to create a VLAN on a bonded interface, like the one just described, and then use that bonded inteface as the physical interface of the vRouter.

To set up virtual functions for the physical interface of a vRouter:


#. Include the ``env.sriov`` section in the ``testbed.py`` file, and complete the following steps to define the SR-IOV virtual functions, so that the virtual functions are created during the provisioning of the cluster.



#. Within ``env.sriov`` , create SR-IOV virtual functions on the compute nodes ( ``host1`` and ``host2`` , in this example). Virtual functions are usually identified with the following naming scheme: ``p6p2_1`` , ``p6p2_2`` , and so on. For example:

   ::

					env.sriov = {

					host1 :[ {'interface' : 'p6p2', 'VF' : 7, 'physnets' : ['physnet1']}],
					host2 :[ {'interface' : 'p6p2', 'VF' : 7, 'physnets’ : ['physnet1']}]

					}




#. Specify the virtual function interfaces in the ``control_data`` section of the ``testbed.py`` file, with or without a VLAN, so that they can be used by the vRouter. For example:

   ::

    control_data = {

     host1 : { 'ip': '10.x.x.100/2x', 'gw' : '10.x.x.254','device':'p6p2_1' }, 
     host2 : { 'ip': '10.x.x.200/2x', 'gw' : '10.x.x.254','device':'p6p2_2' }

     }



#. Optionally, for bonded interfaces ( ``bond0`` in this example), specify the virtual functions in the ``bond`` section of the ``testbed.py`` file, with or without a VLAN. For example:

		::

			bond= {

			host1 : {'name':'bond0','member':['p6p2_4','p6p1_5'],'mode':'balance-xor' },
			host2 : {'name':'bond0','member':['p6p2_2','p6p1_3'],'mode':'balance-xor' }

			}


