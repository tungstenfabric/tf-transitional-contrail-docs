.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

======================
Tungsten Fabric Alerts
======================

Starting with Release 3.0 and greater, Tungsten Fabric alerts are provided on a per-user visible entity (UVE) basis.

Tungsten Fabric analytics raise or clear alerts using Python-coded rules that examine the contents of the UVE and the configuration of the object. Some rules are built in. Others can be added using Python *stevedore* plugins.

This topic describes Tungsten Fabric alerts capabilities.



Alert API Format
----------------

The Tungsten Fabric alert analytics API provides the following:

- Read access to the alerts as part of the UVE GET APIs.


- Alert acknowledgement using POST requests.


- UVE and alert streaming using server-sent events (SSEs).


For example:
GET http://<analytics-ip>:8081/analytics/uves/control-node/a6s40?flat

::

 {
  NodeStatus:  {…},
  ControlCpuState:  {…},
  UVEAlarms:  {
  alarms:  [
      {
          description:  [
              {
              value: "0 != 2",
              rule: "BgpRouterState.num_up_bgp_peer != BgpRouterState.num_bgp_peer"
              }
          ],
          ack: false,
          timestamp: 1442995349253178,
          token: "eyJ0aW1lc3RhbXAiOiAxNDQyOTk1MzQ5MjUzMTc4LCAiaHR0cF9wb3J0Ijog NTk5NSwgImhvc3RfaXAiOiAiMTAuODQuMTMuNDAifQ==",
          type: "BgpConnectivity",
          severity: 4
      }
  ]
  },
  BgpRouterState:  {…}
 }


In the example:

- Alerts are raised on a per-UVE basis and can be retrieved by a GET on a UVE.


- An ``ack`` indicates if the alert has been acknowledged or not.


- A ``token`` is used by clients when requesting acknowledgements




Analytics APIs for Alerts
-------------------------

The following examples show the API to use to display alerts and alarms and to acknowledge alarms.

- To retrieve a list of alerts raised against the control node named ``aXXsYY`` .

::

 GET http://<analytics-ip>:<rest-api-port>/analytics/uves/control-node/aXXsYY&cfilt=UVEAlarms

 This is available for all UVE table types.


- To retrieve a list of all alarms in the system.

::

 GET http://<analytics-ip>:<rest-api-port>/analytics/alarms


- To acknowledge an alarm.

::

 POST http://<analytics-ip>:<rest-api-port>/analytics/alarms/acknowledge
 Body: {“table”: <object-type>,“name”: <key>, “type”: <alarm type>, “token”: <token>}


Acknowledged and unacknowledged alarms can be queried specifically using the following URL query parameters along with the GET operations listed previously.

::

 ackFilt=True
 ackFilt=False





Analytics APIs for SSE Streaming
--------------------------------

The following examples show the API to use to retrieve all or portions of SE streams.

- To retrieve an SSE-based stream of UVE updates for the control node alarms.

::

 GET http://<analytics-ip>:<rest-api-port>/analytics/uve-stream?tablefilt=control-node

 This is available for all UVE table types. If the ``tablefilt`` URL query parameter is not provided, all UVEs are retrieved.


- To retrieve only the alerts portion of the SSE-based stream of UVE updates instead of the entire content.

::

 GET http://<analytics-ip>:<rest-api-port>/analytics/alarm-stream?tablefilt=control-node

::

 This is available for all UVE table types. If the ``tablefilt`` URL query parameter is not provided, all UVEs are retrieved.




Built-in Node Alerts
--------------------

The following built-in node alerts can be retrieved using the APIs listed in *Analytics APIs for Alerts* .

::

 control‐node: {
 PartialSysinfoControl: "Basic System Information is absent for this node in BgpRouterState.build_info",
 ProcessStatus: "NodeMgr reports abnormal status for process(es) in NodeStatus.process_info",
 XmppConnectivity: "Not enough XMPP peers are up in BgpRouterState.num_up_bgp_peer",
 BgpConnectivity: "Not enough BGP peers are up in BgpRouterState.num_up_bgp_peer",
 AddressMismatch: “Mismatch between configured IP Address and operational IP Address",
 ProcessConnectivity: "Process(es) are reporting non‐functional components in NodeStatus.process_status"
 },

 vrouter: {
 PartialSysinfoCompute: "Basic System Information is absent for this node in VrouterAgent.build_info",
 ProcessStatus: "NodeMgr reports abnormal status for process(es) in NodeStatus.process_info",
 ProcessConnectivity: "Process(es) are reporting non‐functional components in NodeStatus.process_status",
 VrouterInterface: "VrouterAgent has interfaces in error state in VrouterAgent.error_intf_list”,
 VrouterConfigAbsent: “Vrouter is not present in Configuration”,
 },

 config‐node: {
 PartialSysinfoConfig: "Basic System Information is absent for this node in ModuleCpuState.build_info",
 ProcessStatus: "NodeMgr reports abnormal status for process(es) in NodeStatus.process_info",
 ProcessConnectivity: "Process(es) are reporting non‐functional components in NodeStatus.process_status"
 },

 analytics‐node: {
 ProcessStatus: "NodeMgr reports abnormal status for process(es) in NodeStatus.process_info"
 PartialSysinfoAnalytics: "Basic System Information is absent for this node in CollectorState.build_info",
 ProcessConnectivity: "Process(es) are reporting non‐functional components in NodeStatus.process_status"
 },

 database‐node: {
 ProcessStatus: "NodeMgr reports abnormal status for process(es) in NodeStatus.process_info",
 ProcessConnectivity: "Process(es) are reporting non‐functional components in NodeStatus.process_status"
 },


