.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================
Understanding Flow Sampling
===========================

This topic describes how flow records are sampled and exported to the Contrail collector, flow handling, and flow aging.

-  `Flow Sampling`_ 


-  `Flow Handling`_ 


-  `Flow Aging`_ 


-  `TCP State-Based Flow Handling and Aging`_ 




Flow Sampling
-------------

The Contrail vRouter agent exports flow records to the Contrail collector when a flow is created or deleted. It also updates flow statistics at regular intervals.

If all flow records are exported from the agent, depending on the scale of flows, some of the exported flows might be dropped due to queue overflow.

In Contrail Release 2.22 and later, to reduce queue overflow, flow records are sampled and exported to the Contrail Collector based on sampling.

The flows that are exported are selected based on the following parameters used in the algorithm:

- The configured flow export rate. This is configured as part of the ``global-vrouter-config`` object.


- The actual flow export rate.


- The sampling threshold. This is a dynamic value calculated internally. If the flow statistics in a flow sample are above this threshold, the flow record is exported.


Each flow is subjected to the following algorithm at regular intervals. The algorithm determines whether to export the sample or not.

- Flows with traffic that is greater than or equal to the sampling threshold are always exported. The byte and packet counts are reported without modification.


- Flows with traffic that is less than the sampling threshold are exported according to the probability. The byte and packet counts are adjusted upwards according to the probability.

The probability is calculated as(bytes during the interval) / (sampling threshold).


- The system generates a random number less than the sampling threshold. If the byte count during the interval is less than the random number, then the flow sample is not exported.


- If none of these conditions are met, the flow sample is exported after normalizing the byte count and packet count during the interval. Normalization is done by dividing the byte count and packet count during the interval by the probability. This normalization is used as a heuristic to account for statistics of flow samples that are dropped.


The actual flow export rate is close to the configured export rate. If there is a large deviation, the sampling threshold is adjusted to bring the actual flow export rate close to the configured flow export rate.



Flow Handling
-------------

When a virtual machine sends or receives IP traffic, forward and reverse flow entries are set up. When the first packet arrives, a flow key is used to hash into a flow table (identify a hash bucket). The flow key is based on five-tuples consisting of source and destination IP addresses, ports, and the IP protocol.

A flow entry is created and the packet is sent to the Contrail vRouter agent. Configured policies are applied and the flow action is updated. The agent also creates a flow entry for the reverse direction where relevant. Subsequent packets match the established flow entries and are forwarded, dropped, NAT translated, and so on, based on the flow action.

When the hash bucket is full, entries are created in an overflow table. In releases earlier than Contrail Release 2.22, the overflow table was a global table, which is searched sequentially. In Contrail Release 2.22 and later, the overflow entries are maintained as a list against the hash bucket.

By default, the maximum number of flow table and overflow table entries are 512,000 and 8000 respectively. These can be modified by configuring them as vRouter module parameters, for example:  vr_flow_entriesand ``vr_oflow_entries`` .

For more information about the vRouter module parameters, see https://github.com/Juniper/contrail-controller/wiki/Vrouter-Module-Parameters .



Flow Aging
----------

Flows are aged out based on inactivity for a specified period of time. By default, the timeout value is 180 seconds. This can be modified by configuring the  flow_cache_timeoutparameter under the ``DEFAULT`` section in the  /etc/contrail/contrail-vrouter-agent.conffile.



TCP State-Based Flow Handling and Aging
---------------------------------------

-  `TCP State-Based Flow Handling`_ 


-  `Protocol-Based Flow Aging`_ 


-  `Fat Flow`_ 




TCP State-Based Flow Handling
-----------------------------

In Contrail Release 2.22 and later, the Contrail vRouter monitors TCP flows to identify entries that can be reused without going through the standard aging cycle.

All flow entries that match TCP flows that have experienced a connection teardown, either through the standard TCP closure cycle (FIN/ACK-FIN/ACK) or the RST indicator, are torn down by the vRouter and are immediately available for use by new qualified flows.

The vRouter also keeps track of connection establishment cycles and exports the necessary information to the vRouter agent, such as SYN/ACK and a digested established flag. This allows the vRouter agent to tear down flows that do not experience a full connection cycle.

Flows that the vRouter identifies as reuse candidates, or eviction candidates, are marked as such in the flow entry. Flows are in the evicted state when they become available for other new flows to be reused.

This two-step transition is used so that the flow entry remains valid until the packet reaches the destination, preventing the flow from getting remapped to another flow entry in the interim.



Protocol-Based Flow Aging
-------------------------

Although TCP flows are deleted based on TCP state, you are sometimes required to age out specific protocol flows more aggressively. One example is when a DNS server is run in one VM. In this case, multiple flows are set up for DNS. A pair of flows are set up to serve each query. Because the flows are no longer required after the query is served, the timeout can be lower for these flows. To handle these cases, protocol-based flow aging is used.

With protocol-based flow aging, the aging timeout can be configured per protocol. All other protocols continue to use the default aging timeout.

Protocol-based flow aging is supported in Contrail Release 2.22 and later.

The configuration for protocol-based flow aging can be done in the ``global-vrouter-config`` object. For example, to have all DNS flows aged out in five seconds, use the following entry: ``protocol = udp, port = 53 will be set an aging timeout of 5 seconds.`` 



Fat Flow
--------

Contrail supports optimization to reduce the number of flows set up by reusing a flow. Consequently, a single flow pair (fat flow) can be used for any number of sessions between two endpoints for the same application protocol.

Any number of DNS sessions from a client to the server can use a single flow pair. The effect is that the flow hash key is reduced from five-tuples to four-tuples, consisting of source and destination IP addresses, the server port, and the IP protocol. The client port is not used in the flow key. Additionally, starting with Contrail 5.0, the hash tuple can be reduced further, to three-tuple or two-tuple.

This feature can be configured by specifying the list of *fat-flow* protocols on a virtual machine interface (VMI). For each such application protocol, the list contains the protocol and port pairs. If you want to enable the fat flow feature on the client side, the configuration must be applied on the client VMI as well.

Starting with Contrail 5.0, fat flow can also be configured at the virtual network (VN) level. When configured at the VN level, the fat flow configuration is applied to all VMIs under the configured VN.

Also starting with Contrail 5.0, fat flow is enhanced with the option to support aggregation of multiple flows into a single flow by ignoring source and destination ports or IP addresses, with the following possible options:

- ignore source and/or destination ports


- ignore source and/or destination IP addresses


- ignore a combination of source and/or destination ports and IP adresses




Configuring Fat Flows
---------------------

The user creates a fat-flow-protocol object, with source and destination options configured, and associates it at the VMI or VN level.

In schema, the ProtocolType object fat-flow-protocol is used to configure if IP addresses or ports are to be ignored, where the value 0 indicates both source and destination ports are to be ignored. Use the virtual-network-fat-flow-protocols for the fat flow object to configure the fat flow at the VN level.

In the Contrail Web UI, to configure fat flow source and destination options at the port, go to **Configure > Networking > Ports** , and edit a port. Select the **Fat-Flows** section and edit the fat flow configuration in the **Ignore Address** field, where the options are **None, Source** , or **Destination** .

To configure fat flow at the VN level, go to **Configure > Networking > Networks** , and select **Edit > Fat Flows** . where you can edit ports and IP addresses to be ignored by the selected network.



Use Case Example
----------------

Consider a simple use case in which traffic from different sources of VN1 goes to the Internet via a service instance (SI). Because each source in VN1 can visit different sites in the Internet, the user might want to ignore all the Internet addresses in the flows.

The following fat flow configurations can achieve this:

Case 1—Source, SI, and destination are in different computes

- Left interface of SI—Ignore source


- Right interface of SI—Ignore destination


Case 2—Source and SI are in same compute, but destination is in different compute

- Source interface—Ignore destination


- Left interface of SI—Ignore source


- Right Interface of SI—Ignore destination


Case 3—Source is in different compute, but SI and destination are in same compute

- LeftiInterface of SI—Ignore source


- Right interface of SI—Ignore destination


- Destination interface—Ignore source




Fat Flow Limitations
--------------------

Fat flow cannot be used when a VMI is ECMP with multiple instances of an ECMP group running on the same compute node.

Fat flow configuration to ignore source or destination address is not supported for NAT flows. This will result in short flows.

**Related Documentation**

-  `Query > Flows`_ 

.. _Query > Flows: monitoring-flow-vnc.html


.. _https://github.com/Juniper/contrail-controller/wiki/Vrouter-Module-Parameters: https://github.com/Juniper/contrail-controller/wiki/Vrouter-Module-Parameters
