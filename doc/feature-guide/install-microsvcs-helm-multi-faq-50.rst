.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=========================================================
Frequently Asked Questions About Contrail and Helm Charts
=========================================================

- How can I make each Contrail service run as a single pod?

 Use the ``manifests.each_container_is_pod=true`` variable to make each Contrail service run as a single pod. Otherwise, all services under control, config, webui, analytics, and vrouter components are grouped into a pod.


- How do I set up the vhost0 interface for the vrouter on the non-management interface of the compute node?


.. note:: Some Contrail versions assume a single name for all of the non-management interfaces in your cluster.



If your non-management interface is ``eth1`` , in the ``contrail-vrouter/values.yaml`` set the ``contrail_env.PHYSICAL_INTERFACE`` to ``eth1`` and set the ``contrail_env.VROUTER_GATEWAY`` to the IP address of the non-management gateway.

::

 # Sample config
 contrail_env:
 CONTROLLER_NODES: 1.1.1.10
 LOG_LEVEL: SYS_NOTICE
 CLOUD_ORCHESTRATOR: openstack
 AAA_MODE: cloud-admin
 PHYSICAL_INTERFACE: eth1
 VROUTER_GATEWAY: 1.1.1.1


- How do I configure the Contrail control BGP server to listen on a different port?

  To configure a non-default BGP port, in the ``contrail-controller/values.yaml`` set the ``contrail_env.BGP`` to the desired port.

  ::

   # Sample config
   contrail_env:
   CONTROLLER_NODES: 1.1.1.10
   LOG_LEVEL: SYS_NOTICE
   CLOUD_ORCHESTRATOR: openstack
   AAA_MODE: cloud-admin
   BGP_PORT: 1179


- How can I pass additional parameters to services in Contrail by using the configuration file in INI format?


.. note:: This example is not valid for WebUI service because its configuration file is in JS format.



For example, to pass the variable ``some_key`` to be in the section ``SOME_SECTION`` of Contrail's service ``SOME_SERVICE`` , add it to the ``contrail_env`` . The service name, section name, and key name are separated by **two** underscore symbols.

::

 # Sample config
 contrail_env:
 SOME_SERVICE__SOME_SECTION__some_key: "value"

 The following example configures the minimum_diskGB parameter for the node manager of the analytics database.

::

 # Sample config
 contrail_env:
 DATABASE_NODEMGR__DEFAULTS__minimum_diskGB: "2"


- How do I configure services for the vrouter agent?

  The following is an example configuration for the vrouter agent.

  ::

   # Sample config
   contrail_env:
   VROUTER_AGENT__FLOWS__thread_count: "2"
   VROUTER_AGENT__METADATA__metadata_use_ssl = True
   VROUTER_AGENT__METADATA__metadata_client_cert = /usr/share/ca-certificates/contrail/client_cert.pem
   VROUTER_AGENT__METADATA__metadata_client_key = /usr/share/ca-certificates/contrail/client_key.pem
   VROUTER_AGENT__METADATA__metadata_ca_cert = /usr/share/ca-certificates/contrail/cacert.pem


- What are the Contrail services that can be configured?

  Configurable services at this time include the following:

   - Configurable services for config node:

     - SVC_MONITOR


     - API


     - DEVICE_MANAGER


     - SCHEMA


     - CONFIG_NODEMGR



   - Configurable services for control:

     - CONTROL


     - DNS


     - CONTROL_NODEMGR



   - Configurable services for analytics:

     - ALARM_GEN


     - TOPOLOGY


     - ANALYTICS_API


     - COLLECTOR


     - SNMP_COLLECTOR


     - QUERY_ENGINE


     - ANALYTICS_NODEMGR


     - Configurable services for database:

       - DATABASE_NODEMGR



     - Configurable services for vrouter:

       - VROUTER_AGENT


       - VROUTER_AGENT_NODEMGR





- How can I pass additional parameters to the Contrail Web UI services a with configuration file in JS format?

  Define the exact variable in the environment. Available configuration settings can be found in the source code, see https://github.com/Juniper/contrail-container-builder/blob/master/containers/controller/webui/base/entrypoint.sh#L31-L199 .
  ::

   # Sample config
   contrail_env:
   WEBUI_SSL_CIPHERS: "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384"


- How can I verify all pods of Contrail are up and running?

  Use the following command to list all pods of Contrail.
  ::

   kubectl get pods -n openstack -o wide | grep contrail-pod



- How can I see the logs of each of the containers?

  Contrail logs are stored under /var/log/contrail/ on each node. To check for the standard output (stdout) log for each container:
  ::

   kubectl logs -f <contrail-pod-name> -n openstack  


- How can I enter into a pod?

  Use the kubectl command.
  ::

   kubectl exec -it <contrail-pod> -n openstack -- bash 


