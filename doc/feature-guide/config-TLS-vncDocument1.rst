.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================================================
Configuring Transport Layer Security-Based XMPP in Contrail
===========================================================



Overview: TLS-Based XMPP
-------------------------

Starting with Contrail 3.0, Transport Layer Security (TLS)-based XMPP can be used to secure all Extensible Messaging and Presence Protocol (XMPP)-based communication that occurs in the Contrail environment.

Secure XMPP is based on *RFC 6120, Extensible Messaging and Presence Protocol (XMPP): Core* .



TLS XMPP in Contrail
--------------------

In the Contrail environment, the Transport Layer Security (TLS) protocol is used for certificate exchange, mutual authentication, and negotiating ciphers to secure the stream from potential tampering and eavesdropping.

The RFC 6120 highlights a basic stream message exchange format for TLS negotiation between an XMPP server and an XMPP client.


.. note:: Simple Authentication and Security Layer (SASL) authentication is not supported in the Contrail environment.





Configuring XMPP Client and Server in Contrail
----------------------------------------------

In the Contrail environment, XMPP based communications are used in client and server exchanges, between the compute node (as the XMPP client), and:

   - the control node (as the XMPP server)


   - the DNS server (as the XMPP server)




Configuring Control Node for XMPP Server
----------------------------------------

To enable secure XMPP, the following parameters are configured at the XMPP server.

On the control node, enable the parameters in the configuration file: ``/etc/contrail/contrail-control.conf`` .

+-----------------------+-----------------------+-----------------------+
| Parameter             | Description           | Default               |
+=======================+=======================+=======================+
| xmpp_server_cert      | Path to the node's    | /etc/contrail/ssl/cer |
|                       | public certificate    | ts/server.pem         |
+-----------------------+-----------------------+-----------------------+
| xmpp_server_key       | Path to server's or   | /etc/contrail/ssl/pri |
|                       | node's private key    | vate/server-privkey.p |
|                       |                       | em                    |
+-----------------------+-----------------------+-----------------------+
| xmpp_ca_cert          | Path to CA            | /etc/contrail/ssl/cer |
|                       | certificate           | ts/ca-cert.pem        |
+-----------------------+-----------------------+-----------------------+
| xmpp_auth_enable=true | Enables SSL based     | Default is set to     |
|                       | XMPP                  | false, XMPP is        |
|                       |                       | disabled.             |
|                       |                       |                       |
|                       |                       | **Note:** The keyword |
|                       |                       | true is case          |
|                       |                       | sensitive.            |
+-----------------------+-----------------------+-----------------------+





Configuring DNS Server for XMPP Server
--------------------------------------

To enable secure XMPP, the following parameters are configured at the XMPP DNS server.

On the DNS server control node, enable the parameters in the configuration file: ``/etc/contrail/contrail-control.conf`` 

+-----------------------+-----------------------+-----------------------+
| Parameter             | Description           | Default               |
+=======================+=======================+=======================+
| xmpp_server_cert      | Path to the node's    | /etc/contrail/ssl/cer |
|                       | public certificate    | ts/server.pem         |
+-----------------------+-----------------------+-----------------------+
| xmpp_server_key       | Path to               | /etc/contrail/ssl/cer |
|                       | server's/node's       | ts/server-privkey.pem |
|                       | private key           |                       |
+-----------------------+-----------------------+-----------------------+
| xmpp_ca_cert          | Path to CA            | /etc/contrail/ssl/cer |
|                       | certificate           | ts/ca-cert.pem        |
+-----------------------+-----------------------+-----------------------+
| xmpp_dns_auth_enable= | Enables SSL based     | Default is set to     |
| true                  | XMPP                  | false, XMPP is        |
|                       |                       | disabled.             |
|                       |                       |                       |
|                       |                       | **Note:** The keyword |
|                       |                       | true is case          |
|                       |                       | sensitive.            |
+-----------------------+-----------------------+-----------------------+



Configuring Control Node for XMPP Client
----------------------------------------

To enable secure XMPP, the following parameters are configured at the XMPP client.

On the compute node, enable the parameters in the configuration file: ``/etc/contrail/contrail-vrouter-agent.conf`` 

+-----------------------+-----------------------+-----------------------+
| Parameter             | Description           | Default               |
+=======================+=======================+=======================+
| xmpp_server_cert      | Path to the node's    | /etc/contrail/ssl/cer |
|                       | public certificate    | ts/server.pem         |
+-----------------------+-----------------------+-----------------------+
| xmpp_server_key       | Path to               | /etc/contrail/ssl/pri |
|                       | server's/node's       | vate/server-privkey.p |
|                       | private key           | em                    |
+-----------------------+-----------------------+-----------------------+
| xmpp_ca_cert          | Path to CA            | /etc/contrail/ssl/cer |
|                       | certificate           | ts/ca-cert.pem        |
+-----------------------+-----------------------+-----------------------+
| xmpp_auth_enable=true | Enables SSL based     | Default is set to     |
| xmpp_dns_auth_enable= | XMPP                  | false, XMPP is        |
| true                  |                       | disabled.             |
|                       |                       |                       |
|                       |                       | **Note:** The keyword |
|                       |                       | true is case          |
|                       |                       | sensitive.            |
+-----------------------+-----------------------+-----------------------+



