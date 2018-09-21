.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============
Known Behavior
==============

This section lists known limitations with this release. Bug numbers are listed and can be researched in `Launchpad.net`_  at `https://bugs.launchpad.net/juniperopenstack`_  .

-  `Known Behavior in Contrail Release 5.0.1`_ 


-  `Known Behavior in Contrail Release 5.0`_ 


Known Behavior in Contrail Release 5.0.1
----------------------------------------

- 1628326 DPDK-based compute node may not handle ARP packets correctly if only one CPU core is assigned to the vRouter in the test bed file.


- 1694343 In DPDK vRouter use cases such as SNAT and LBaaS that require netns, you cannot set jumbo MTU size. Maximum MTU allowed: <=1500 . There is no workaround at present.


- 1714063 Analytics services does not support Keystone V3.


- 1716308 When the vRouter receives the head fragment of an ICMPv6 packet, the head fragment is immediately enqueued to the assembler. The flow is created as hold flow and then trapped to the agent. If fragments corresponding to this head fragment are already in the assembler or if new fragments arrive immediately after the head fragment, the assembler releases them to flow module. Fragments get enqueued in the hold queue if agent does not write flow action by the time the assembler releases fragments to the flow module. A maximum of three fragments are enqueued in the hold queue at a time. The remaining fragments are dropped from the assembler to the flow module.

 As a workaround, the head fragment is enqueued to assembler only after flow action is written by agent. If the flow is already present in non-hold state, it is immediately enqueued to assembler.


- 1730021 In Contrail Security, non-admin users cannot access global scope objects when  ``global_access`` is set to  ``0``.

 As a workaround, for non-admin users to access global scope objects, set  ``global_access`` to  ``5``.


- 1733027 In a multi-node analytics cluster, when one of analytics nodes shuts down or is rebooted, the contrail-status on the other analytics nodes displays the status of contrail-analytics-api and contrail-alarm-gen as initializing with the error message:  ``Redis-UVE:<ip-address of analytics node that was shutdown/rebooted>:6381[None] connection down``. This does not impact the functioning of the analytics cluster.


- 1735057 When bringing up Contrail cluster on Red Hat container, manually install docker-py on all the target nodes.

  - To install Pip, use the following command:
    ::

     wget https://bootstrap.pypa.io/get-pip.py python get-pip.py


  - To install docker-py, use the following command:
    ::

     pip install docker-py

- 1749614 In a Helm-based provisioned cluster, VM launch fails if MariaDB replication is set to >1.


- 1754742 When you receive an error message during Kolla provisioning, rerunning the code will not work. In order for the provisioning to work, restart provisioning from scratch.


- 1755997 Kubernetes IP fabric feature is supported only on the pods and not the services.


- 1759428 Cannot provision an external MX series router by running the  provision_mx.pyscript that contains the list of external routers.


- 1759576 Metadata SSL works only in HA deployment mode.


- 1759695 After deleting a vRouter chart with DPDK, the NICS do not rebind to the host in Helm.


- 1761137 High Availability provisioning of Kubernetes master is not supported.


- 1764610 Ansible-deployer: DPDK PPS is low.


- 1764739 Docker restart hangs indefinitely and Docker daemon stops running post the hang.


- 1765281 On a DPDK compute  vif list –ratecore-dumps with traffic.


- 1766035 On a Kubernetes cluster, a controller node reboot fails to re-establish the BGP XMPP connection with compute nodes. As a workaround, flush the iptables on the Kubernetes master.


- 1766315 After provisioning Contrail by using a Helm-based provisioned cluster, restart nova-compute container.


- 1767472 SR-IOV with DPDK co-existence deployment is not supported using contrail-helm-deployer.


- 1771444 CFM: The MTU on devices between the IRONIC node and BMS must be manually configured accounting for the VxLAN encapsulation that carries traffic between them.


- 1777562 CFM: CSN HA is not supported


- 1778279 CFM: ESI Multihoming with multiple interfaces connected to the same ESI (same TOR) is not supported.


- 1781305 OpenShift deployer code does not have the option to choose different interface names for different physical nodes.


- 1782067 CFM: BGP peering configuration from an existing device is not removed while unassigning the physical device.


- 1784085 OpenShift deployments do not install NTP on the nodes. After provisioning, you must install and start the ntpd on all Openshift nodes manually.


- 1784750 Contrail RBAC (API and analytics) policies are not part of Contrail Helm charts unlike in OpenStack components. You cannot override global/domain/project RBAC policies while deploying Helm charts.


- 1785448 You cannot configure routing tables on the Contrail Command UI. Routing tables must be configured on the older Contrail UI at **Networking > Routing** .


- 1785925 CFM: Upon deletion of device images, a few chunks remain in the image repository.


- 1786102 CFM: In Contrail Release 5.0.1 release, interface channelization of devices in greenfield workflow is not supported. In brownfield, interface channelization is supported as long as it is configured manually before onboarding devices.


- 1786348 Contrail-Command: Token expires immediately after clicking **Create Instance** on the UI. This causes the instance to be present in the UI, but entire data does not get pushed in the backend.


- 1786354 CFM: Unassigning and reassigning the device to fabric doesn't reconfigure the QFX with Contrail configuration.


- 1786536 CFM: For auto configure of devices to be successful, while adding the devices, both physical and overlay roles must be specified.


- 1786487 Dynamic mirroring without Juniper header does not work for VxLAN encapsulation.


- 1786511 rabbitmq cluster formation fails during Helm sanity job. As a workaround, update the rabbitmq section of the ``contrail-analytics/values.yaml`` and ``contrail-controller/values.yaml`` files, to include the IP addresses of the controller nodes. For example, change ``endpoints.rabbitmq.hosts.default: rabbitmq`` to ``endpoints.rabbitmq.hosts.default: "controller_node1_IP,controller_node2_IP,controller_node3_IP"`` .


- 1786527 In Helm-based provisioning when the vRouter gets provisioned, the vRouter gets disconnected from other vRouters residing on different subnets. As a workaround, move the host routes used to reach different subnets to vhost0 interface and restart the system.


- 1786560 In Kubernetes single yaml file-based provisioning, when the vRouter gets provisioned, the vRouter gets disconnected from other vRouters residing on different subnets. As a workaround, move the host routes used to reach different subnets to vhost0 interface and restart the system.


- 1786836 CFM: Logical Router pushed to spine devices during device role assignment will not allow VxLAN routing to be enabled. To prevent this situation, configure VxLAN routing on spines before assigning the spine role on a physical router


- 1786855 CFM: BMS - LAG can be configured on a BMS only if life cycle management is executed through CFM.


- 1786856 Fabric device discovery fails intermittently in the Contrail HA topology. As a workaround, restart Config_api_1 on all HA nodes and run device discovery again.


- 1787303 Contrail Release 5.0.1 uses DPDK version 17.11.03, DPDK vRouter using uio driver as vfio-pci, typically for Intel Fortville NICs, and needs firmware upgrade to the following version or later (if it is certified by users).

	driver: i40e

	version: 2.1.14-k

	firmware-version: 6.01 0x80003493 255.65535.255


- 1789768 Instances.yml in the contrail_command container is populated with the default password instead of the one provided by the user.




Known Behavior in Contrail Release 5.0
--------------------------------------

- 1694343 In DPDK vRouter use cases such as SNAT and LBaaS that require netns, you cannot set jumbo MTU size. Maximum MTU allowed: <=1500 . There is no workaround at present.


- 1716308 When the vRouter receives the head fragment of an ICMPv6 packet, the head fragment is immediately enqueued to the assembler. The flow is created as hold flow and then trapped to the agent. If fragments corresponding to this head fragment are already in the assembler or if new fragments arrive immediately after the head fragment, the assembler releases them to flow module. Fragments get enqueued in the hold queue if agent does not write flow action by the time the assembler releases fragments to the flow module. A maximum of three fragments are enqueued in the hold queue at a time. The remaining fragments are dropped from the assembler to the flow module.

 As a workaround, the head fragment is enqueued to assembler only after flow action is written by agent. If the flow is already present in non-hold state, it is immediately enqueued to assembler.


- 1730021 In Contrail Security, non-admin users cannot access global scope objects when  global_accessis set to  0.

 As a workaround, for non-admin users to access global scope objects, set  global_accessto  5.


- 1733027 In a multi-node analytics cluster, when one of analytics nodes shuts down or is rebooted, the contrail-status on the other analytics nodes displays the status of contrail-analytics-api and contrail-alarm-gen as initializing with the error message:  Redis-UVE:<ip-address of analytics node that was shutdown/rebooted>:6381[None] connection down. This does not impact the functioning of the analytics cluster.


- 1735590 In Kubernetes and OpenShift based deployments when we crate SNAT router and extend cluster-network to that SNAT router host is losing all connectivity.

 As a workaround, if you want to use the SNAT feature in Contrail, disassociate the ip-fabric-cluster-network-default policy and delete it.


- 1749614 In a Helm-based provisioned cluster, VM launch fails if MariaDB replication is set to >1.


- 1754742 When you receive an error message during Kolla provisioning, rerunning the code will not work. In order for the provisioning to work, restart provisioning from scratch.


- 1755997 Kubernetes IP fabric feature is supported only on the pods and not the services.


- 1759576 Metadata SSL works only in HA deployment mode.


- 1759695 After deleting a vRouter chart with DPDK, the NICS do not rebind to the host in Helm.


- 1761137 High Availability provisioning of Kubernetes master is not supported.


- 1764739 Docker restart hangs indefinitely and Docker daemon stops running post the hang.


- 1764925 RabbitMQ clustering fails on certain nodes in a setup. As a workaround, restart the container that is not in the cluster.


- 1765277 When a snapshot of an active VM fails, shutdown the VM before generating the snapshot.


- 1765281 On a DPDK compute  ``vif list –rate`` core-dumps with traffic.


- 1765487 A false alarm for config service is generated when  ``config`` and  ``configdb`` services are installed on different nodes. Ignore the false alarm.


- 1766035 On a Kubernetes cluster, a controller node reboot fails to re-establish the BGP XMPP connection with compute nodes. As a workaround, flush the iptables on the Kubernetes master.


- 1766315 After provisioning Contrail by using a Helm-based provisioned cluster, restart nova-compute container.


- 1766371 OpenShift use cases work in non-HA environments only.


- 1767094 Kube DNS fails to come online come up in a multi-interface setup.


- 1767466 In Contrail 5.0 release, with Contrail Helm charts, Kubernetes ingress Web UI URL does not work when Web UI is started with secure (TLS) option.


- 1767470 SR-IOV installation is not supported with contrail-helm-deployer.


- 1767472 SR-IOV with DPDK co-existence deployment is not supported using contrail-helm-deployer.


- 1759428 Cannot provision an external MX series router by running the  ``provision_mx.py`` script that contains the list of external routers.



.. _Launchpad.net: https://bugs.launchpad.net/​

.. _https://bugs.launchpad.net/juniperopenstack: https://bugs.launchpad.net/juniperopenstack
