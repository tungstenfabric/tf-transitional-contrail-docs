.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===================================================================================
Configuring the Data Plane Development Kit (DPDK) Integrated with Contrail vRouter
===================================================================================

-  `DPDK Support in Contrail​`_ 


-  `Preparing the Environment File for Provisioning a Cluster Node with DPDK`_ 


-  `Creating a Flavor for DPDK in OpenStack Kilo`_ 




DPDK Support in Contrail​
--------------------------

Contrail 3.0 and later supports the Data Plane Development Kit (DPDK) on Ubuntu systems, only.

DPDK is an open source set of libraries and drivers for fast packet processing. DPDK enables fast packet processing by allowing network interface cards (NICs) to send direct memory access (DMA) packets directly into an application’s address space, allowing the application to poll for packets, and thereby avoiding the overhead of interrupts from the NIC.

Integrating with DPDK allows a Contrail vRouter to process more packets per second than is possible when running as a kernel module.

When using DPDK with Contrail 4.0, one or more Contrail compute nodes are provisioned with DPDK during installation. An entry in the server configuration file specifies which nodes are to be configured to use the DPDK vRouter mode instead of the regular kernel mode. This allows for a mixed setup, where different nodes use different modes of the vRouter.

Upon installation, when a Contrail compute node is provisioned with DPDK, the server configuration file specifies which physical interface(s) to use, how many CPU cores to use for forwarding packets, and the number of huge pages to allocate for DPDK.



Preparing the Environment File for Provisioning a Cluster Node with DPDK
------------------------------------------------------------------------

The environment file is used at provsioning to specify all of the options necessary for the installation of a Contrail cluster, including whether any node should be configured to use DPDK.

Each node to be configured with the DPDK vRouter must be listed in the provisioning file with a dictionary entry, along with the percentage of memory for DPDK huge pages and the CPUs to be used.

The following are descriptions of the required entries for the server configuration. :

-  ``huge_pages`` —Specify the percentage of host memory to be reserved for the DPDK huge pages. The reserved memory will be used by the vRouter and the Quick Emulator (QEMU) for allocating memory resources for the virtual machines (VMs) spawned on that host.


.. note:: The percentage allocated to ``huge_pages`` should not be too high, because the host Linux kernel also requires memory.




-  ``coremask`` —Specify a CPU affinity mask with which vRouter will run. vRouter will use only the CPUs specified for its threads of execution. These CPU cores will be constantly polling for packets, and they will be displayed as 100% busy in the output of “top”.

Supported formats include:

- Hexadecimal (for example, 0xf)


- Comma-separated list of CPUs (1,2,4...)


- Dash-separated range of CPUs (for example, 1-4)



The server configuration file is configured prior to the installation of Contrail.

Use the standard Contrail installation procedure, and upon completion, your cluster with specified nodes using the DPDK vRouter implementation is ready to use.



Support for Multiple UIO Drivers
--------------------------------

Support is available for optionally specifying the userspace IO (UIO) driver to use in a DPDK-enabled compute node.
Specify UIO in the ``dpdk`` section of the server configuration file, by using the optional attribute ``uio_driver`` :

::

   {
  "server" : [{
    "parameters" : {
      "provision": {
        "contrail_4": {
          "core_mask": "0x3f",
          "huge_pages": "50",
          "uio_driver" : "igb_uio"
        }
      }
    }
  }]
 }


The supported values for ``uio_driver`` include:

-  ``igb_uio`` —specify that the igb_uio module from the DPDK library should be used.


-  ``vfio-pci`` —specify that the vfio module in the Linux kernel should be used instead of uio, which protects memory accesses using the IOMMU when a SR-IOV virtual function is used as the physical interface of vrouter.


-  ``uio_pci_generic`` —specify that the UIO driver that is built into the Linux kernel should be used. This option does not support the use of SR-IOV VFs.


If the ``uio_driver`` is not specified in the server configuration file, ``igb_uio`` is used by default.



Creating a Flavor for DPDK in OpenStack Kilo
--------------------------------------------

OpenStack Kilo has a feature called flavors, which are virtual hardware templates that define sizes for RAM, disk, and so on. Contrail 3.0 and later supports the OpenStack Kilo flavor that specifies that a VM should use huge pages. The use of huge pages is a requirement for using a DPDK vRouter.
Use the following command to add the flavor, where ``m1.large`` is the name of the flavor. When a VM is created using this flavor, OpenStack ensures that the VM will only be spawned on a compute node that has huge pages enabled.

::

 $nova flavor-key m1.large set hw:mem_page_size=large  

Huge pages are enabled for compute nodes where vRouter is provisioned with DPDK.

If a VM is spawned with a flavor that does not have huge pages enabled, the VM should not be created on a compute node on which vRouter is provisioned with DPDK.

You can use OpenStack availability zones or host aggregates to exclude the hosts where vRouter is provisioned with DPDK.

**Related Documentation**

-  `Configuring Single Root I/O Virtualization (SR-IOV)`_ 

- DPDK official page: http://www.dpdk.org

.. _Configuring Single Root I/O Virtualization (SR-IOV): sriov-with-vrouter-vnc.html

