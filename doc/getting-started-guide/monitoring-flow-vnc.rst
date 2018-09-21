.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=============
Query > Flows
=============

Select **Query > Flows** to perform rich and complex SQL-like queries on flows in the Contrail Controller. You can use the query results for such things as gaining insight into the operation of applications in a virtual network, performing historical analysis of flow issues, and pinpointing problem areas with flows.

-  `Query > Flows > Flow Series`_ 


-  `Example: Query Flow Series`_ 


-  `Query > Flow Records`_ 


-  `Query > Flows > Query Queue`_ 



Query > Flows > Flow Series
===========================

Select **Query > Flows > Flow Series** to create queries of the flow series table. The results are in the form of time series data for flow series. See `Figure 111`_ 

.. _Figure 111: 

*Figure 111* : Query Flow Series Window

.. figure:: s041598.gif

The query fields available on the screen for the **Flow Series** tab are described in `Table 45`_ . Enter query data into the fields to create a SQL-like query to display and analyze flows.

.. _Table 45: 


*Table 45* : Query Flow Series Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Time Range**                    | Select a range of time to display |
|                                   | the flow series:                  |
|                                   |                                   |
|                                   | -  Last 10 Mins                   |
|                                   | -  Last 30 Mins                   |
|                                   | -  Last 1 Hr                      |
|                                   | -  Last 6 Hrs                     |
|                                   | -  Last 12 Hrs                    |
|                                   | -  Custom                         |
|                                   |                                   |
|                                   | Click **Custom** to enter a       |
|                                   | specific custom time range in two |
|                                   | fields: **From Time** and **To    |
|                                   | Time**.                           |
+-----------------------------------+-----------------------------------+
| **Select**                        | Click the edit button (pencil     |
|                                   | icon) to open a **Select** window |
|                                   | (`Figure 112`_), where you can    |
|                                   | click one or more boxes to select |
|                                   | the fields to display from the    |
|                                   | flow series, such as **Source VN, |
|                                   | Dest VN, Bytes, Packets**, and    |
|                                   | more.                             |
+-----------------------------------+-----------------------------------+
| **Where**                         | Click the edit button (pencil     |
|                                   | icon) to open a query-writing     |
|                                   | window, where you can specify     |
|                                   | query values for variables such   |
|                                   | as **sourcevn, sourceip, destvn,  |
|                                   | destip, protocol, sport, dport**. |
+-----------------------------------+-----------------------------------+
| **Direction**                     | Select the desired flow           |
|                                   | direction: **INGRESS** or         |
|                                   | **EGRESS**.                       |
+-----------------------------------+-----------------------------------+
| **Filter**                        | Click the edit button (pencil     |
|                                   | icon) to open a **Filter** window |
|                                   | (`Figure 113`_), where you can    |
|                                   | select filter items to sort by,   |
|                                   | the sort order, and limits to the |
|                                   | number of results returned.       |
+-----------------------------------+-----------------------------------+
| **Run Query**                     | Click **Run Query** to retrieve   |
|                                   | the flows that match the query    |
|                                   | you created. The flows are listed |
|                                   | on the lower portion of the       |
|                                   | screen in a box with columns      |
|                                   | identifying the selected fields   |
|                                   | for each flow.                    |
+-----------------------------------+-----------------------------------+
| (graph buttons)                   | When **Time Granularity** is      |
|                                   | selected, you have the option to  |
|                                   | view results in graph or          |
|                                   | flowchart form. Graph buttons     |
|                                   | appear on the screen above the    |
|                                   | **Export** button. Click a graph  |
|                                   | button to transform the tabular   |
|                                   | results into a graphical chart    |
|                                   | display.                          |
+-----------------------------------+-----------------------------------+
| **Export**                        | The Export button is displayed    |
|                                   | after you click **Run Query**.    |
|                                   | This allows you to export the     |
|                                   | list of flows to a text .csv      |
|                                   | file.                             |
+-----------------------------------+-----------------------------------+

The **Select** window allows you to select one or more attributes of a flow series by clicking the check box for each attribute desired, see `Figure 112`_ . The upper section of the **Select** window includes field names, and the lower portion lets you select units. Select **Time Granularity** and then select **SUM(Bytes)** or **SUM(Packets)** to aggregate bytes and packets in intervals.

.. _Figure 112: 

*Figure 112* : Flow Series Select

.. figure:: s041600.gif

Use the **Filter** window to refine the display of query results for flows, by defining an attribute by which to sort the results, the sort order of the results, and any limit needed to restrict the number of results. See `Figure 113`_ .

.. _Figure 113: 

*Figure 113* : Flow Series Filter

.. figure:: s041599.gif


Example: Query Flow Series
==========================

The following is an example flow series query that returns the time series of the summation traffic in bytes for all combinations of source VN and destination VN for the last 10 minutes, with the bytes aggregated in 10 second intervals. See `Figure 114`_ .

.. _Figure 114: 

*Figure 114* : Example: Query Flow Series

.. figure:: s041604.gif

The query returns tabular time series data, see `Figure 115`_ , for the following combinations of Source VN and Dest VN:

- Flow Class 1: Source VN = default-domain:demo:front-end, Dest VN=__UNKNOWN__


- Flow Class 2: Source VN = default-domain:demo:front-end, Dest VN=default-domain:demo:back-end


.. _Figure 115: 

*Figure 115* : Query Flow Series Tabular Results

.. figure:: s041605.gif

Because **Time Granularity** is selected, the results can also be displayed as graphical charts. Click the graph button on the right side of the tabular results. The results are displayed in a graphical flow chart. See `Figure 116`_ .

.. _Figure 116: 

*Figure 116* : Query Flow Series Graphical Results

.. figure:: s041611.gif


Query > Flow Records
====================

Select **Query > Flow Records** to create queries of individual flow records for detailed debugging of connectivity issues between applications and virtual machines. Queries at this level return records of the active flows within a given time period.

.. _Figure 117: 

*Figure 117* : Flow Records

.. figure:: s041601.gif

The query fields available on the screen for the **Flow Records** tab are described in `Table 46`_ . Enter query data into the fields to create an SQL-like query to display and analyze flows.

.. _Table 46: 


*Table 46* : Query Flow Records Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Time Range**                    | Select a range of time for the    |
|                                   | flow records:                     |
|                                   |                                   |
|                                   | -  Last 10 Mins                   |
|                                   | -  Last 30 Mins                   |
|                                   | -  Last 1 Hr                      |
|                                   | -  Last 6 Hrs                     |
|                                   | -  Last 12 Hrs                    |
|                                   | -  Custom                         |
|                                   |                                   |
|                                   | Click **Custom** to enter a       |
|                                   | specified custom time range in    |
|                                   | two fields: **From Time** and     |
|                                   | **To Time**.                      |
+-----------------------------------+-----------------------------------+
| **Select**                        | Click the edit button (pencil     |
|                                   | icon) to open a **Select** window |
|                                   | (`Figure 118`_), where you can    |
|                                   | click one or more boxes to select |
|                                   | attributes to display for the     |
|                                   | flow records, including **Setup   |
|                                   | Time, Teardown Time, Aggregate    |
|                                   | Bytes,** and **Aggregate          |
|                                   | Packets**.                        |
+-----------------------------------+-----------------------------------+
| **Where**                         | Click the edit button (pencil     |
|                                   | icon) to open a query-writing     |
|                                   | window where you can specify      |
|                                   | query values for **sourcevn,      |
|                                   | sourceip, destvn, destip,         |
|                                   | protocol, sport, dport**. .       |
+-----------------------------------+-----------------------------------+
| **Direction**                     | Select the desired flow           |
|                                   | direction: **INGRESS** or         |
|                                   | **EGRESS**.                       |
+-----------------------------------+-----------------------------------+
| **Run Query**                     | Click **Run Query** to retrieve   |
|                                   | the flow records that match the   |
|                                   | query you created. The records    |
|                                   | are listed on the lower portion   |
|                                   | of the screen in a box with       |
|                                   | columns identifying the fields    |
|                                   | for each flow.                    |
+-----------------------------------+-----------------------------------+
| **Export**                        | The **Export** button is          |
|                                   | displayed after you click **Run   |
|                                   | Query**, allowing you to export   |
|                                   | the list of flows to a text       |
|                                   | ``.csv`` file.                    |
+-----------------------------------+-----------------------------------+

The **Select** window allows you to select one or more attributes to display for the flow records selected, see `Figure 118`_ .

.. _Figure 118: 

*Figure 118* : Flow Records Select Window

.. figure:: s041602.gif

You can restrict the query to a particular source VN and destination VN combination using the **Where** section.

The **Where Clause** supports logical AND and logical OR operations, and is modeled as a logical OR of multiple AND terms. For example: ( (term1 AND term2 AND term3..) OR (term4 AND term5) OR…).

Each term is a single variable expression such as **Source VN = VN1** .

.. _Figure 119: 

*Figure 119* : Where Clause Window

.. figure:: s041608.gif


Query > Flows > Query Queue
===========================

Select **Query > Flows > Query Queue** to display queries that are in the queue waiting to be performed on the data. See `Figure 120`_ .

.. _Figure 120: 

*Figure 120* : Flows Query Queue

.. figure:: s041592.gif

The query fields available on the screen for the **Flow Records** tab are described in `Table 47`_ . Enter query data into the fields to create an SQL-like query to display and analyze flows.

.. _Table 47: 


*Table 47* : Query Flow Records Fields

+-----------------------------------+-----------------------------------+
| Field                             | Description                       |
+===================================+===================================+
| **Date**                          | The date and time the query was   |
|                                   | started.                          |
+-----------------------------------+-----------------------------------+
| **Query**                         | A display of the parameters set   |
|                                   | for the query.                    |
+-----------------------------------+-----------------------------------+
| **Progress**                      | The percentage completion of the  |
|                                   | query to date.                    |
+-----------------------------------+-----------------------------------+
| **Records**                       | The number of records matching    |
|                                   | the query to date.                |
+-----------------------------------+-----------------------------------+
| **Status**                        | The status of the query, such as  |
|                                   | **completed**.                    |
+-----------------------------------+-----------------------------------+
| **Time Taken**                    | The amount of time in seconds it  |
|                                   | has taken the query to return the |
|                                   | matching records.                 |
+-----------------------------------+-----------------------------------+
| (Action icon)                     | Click the **Action** icon and     |
|                                   | select **View Results** to view a |
|                                   | list of the records that match    |
|                                   | the query, or click **Delete** to |
|                                   | remove the query from the queue.  |
+-----------------------------------+-----------------------------------+

**Related Documentation**

- Understanding Flow Sampling

