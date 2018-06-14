.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

================================================================
Configuring Secure Sandesh and Introspect for Contrail Analytics
================================================================

-  `Configuring Secure Sandesh Connection`_ 


-  `Configuring Secure Introspect Connection`_ 




Configuring Secure Sandesh Connection
-------------------------------------

All Contrail services use Sandesh, a southbound interface protocol based on Apache Thrift, to send analytics data such as system logs, object logs, UVEs, flow logs, and the like, to the collector service in the Contrail Analytics node. The Transport Layer Security (TLS) protocol is used for certificate exchange, mutual authentication, and negotiating ciphers to secure the Sandesh connection from potential tampering and eavesdropping.

To configure a secure Sandesh connection, configure the following parameters in all Contrail services that connect to the collector (Sandesh clients) and the Sandesh server.

+-----------------------+-----------------------+-----------------------+
| Parameter             | Description           | Default               |
+=======================+=======================+=======================+
| [SANDESH].sandesh_key | Path to the node's    | ``/etc/contrail/ssl/p |
| file                  | private key           | rivate/server-privkey |
|                       |                       | .pem``                |
+-----------------------+-----------------------+-----------------------+
| [SANDESH].sandesh_cer | Path to the node's    | ``/etc/contrail/ssl/c |
| tfile                 | public certificate    | erts/server.pem``     |
+-----------------------+-----------------------+-----------------------+
| [SANDESH].sandesh_ca_ | Path to the CA        | ``/etc/contrail/ssl/c |
| cert                  | certificate           | erts/ca-cert.pem``    |
+-----------------------+-----------------------+-----------------------+
| [SANDESH].sandesh_ssl | Enable or disable     | ``false``             |
| _enable               | secure Sandesh        |                       |
|                       | connection            |                       |
+-----------------------+-----------------------+-----------------------+


Configuring Secure Introspect Connection
----------------------------------------

All Contrail services are embedded with a web server that can be used to query the internal state of the data structures, view trace messages, and perform other extensive debugging. The Transport Layer Security (TLS) protocol is used for certificate exchange, mutual authentication, and negotiating ciphers to secure the introspect connection from potential tampering and eavesdropping.

To configure a secure introspect connection, configure the following parameters in the Contrail service, see `Table 36`_ .

.. _Table 36: 


*Table 36* : Secure Introspect Parameters

+-----------------------+-----------------------+-----------------------+
| Parameter             | Description           | Default               |
+=======================+=======================+=======================+
| [SANDESH].sandesh_key | Path to the node's    | ``/etc/contrail/ssl/p |
| file                  | private key           | rivate/server-privkey |
|                       |                       | .pem``                |
+-----------------------+-----------------------+-----------------------+
| [SANDESH].sandesh_cer | Path to the node's    | ``/etc/contrail/ssl/c |
| tfile                 | public certificate    | erts/server.pem``     |
+-----------------------+-----------------------+-----------------------+
| [SANDESH].sandesh_ca_ | Path to the CA        | ``/etc/contrail/ssl/c |
| cert                  | certificate           | erts/ca-cert.pem``    |
+-----------------------+-----------------------+-----------------------+
| [SANDESH].introspect_ | Enable or disable     | ``false``             |
| ssl_enable            | secure introspect     |                       |
|                       | connection            |                       |
+-----------------------+-----------------------+-----------------------+

