.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================
More Efficient Flow Queries
===========================



Flow queries are now analyzed on a 7-tuple basis, enabling more efficient flow queries by focusing on elements more important for analysis, and de-emphasizing lesser elements. More efficient queries enable load reduction and allow application of security policy.

An enhanced security framework is implemented to manage connectivity between workloads, or VMIs. Each VMI is tagged with the attributes of Deployment, App, Tier, and Site, and the user specifies security policies for VMIs using the values of these tags. Contrail can analyze the traffic flow between groups of VMI, where groups are categorized according to one or more values of the tags.

The existing FlowLogData is replaced by SessionEndpointData, which is a combination of the local VMI tags and VNs, the security policy and security rule, and route attributes for the remote endpoint. A SessionAggregate map and counts both enable traffic analysis within and across security policies by means of session sampling and session aggregate counts.

The flow export feature is disabled by default. Until the session_export_rate is set explicitly, flow queries will not return any results regardless of the traffic. To use this feature, set the session export rate in the Contrail WebUI at **Config->Global Config->Forwarding Options** .

