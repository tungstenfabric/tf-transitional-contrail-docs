.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================================================
Configuring Contrail DPDK vRouter to Run in a Docker Container
==============================================================

Starting with Contrail Release 5.0, you can configure the Contrail DPDK vRouter to run in a Docker container. In earlier releases, DPDK vRouter runs on a compute host. The contrail-vrouter-dpdk binary file provides data plane functionality when Contrail vRouter runs in DPDK mode in a Contrail cluster.

Complete these steps to configure Contrail DPDK vRouter to run in a Docker container.


#. Run the following commands on the compute host:
   
   ::

    edit /etc/sysctl.conf and add below paramteres a.vm.nr_hugepages = 48341 b.vm.max_map_count = 96682 c.kernel.core_pattern = /var/crashes/core.%e.%p.%h.%t 
    mkdir -p /hugepages 
    echo “hugetlbfs /hugepages hugetlbfs defaults 0 0 “ >> /etc/fstab 4.sudo mount -t hugetlbfs hugetlbfs /hugepages


#. Perform the following steps on the Docker container:

   - Install pciutils.


   - Install the following packages in the container:

     - contrail-vrouter-dpdk-init


     - contrail-vrouter-dpdk


     - contrail-vrouter-utils


     - python-opencontrail-vrouter-netns


     - python-contrail-vrouter-api


#. Run the following commands:

::

  /opt/contrail/bin/dpdk_nic_bind.py -b ixgbe 0000:02:00.0 
 /opt/contrail/bin/dpdk_nic_bind.py -s 
 taskset 0xf /usr/bin/contrail-vrouter-dpdk --no-daemon


