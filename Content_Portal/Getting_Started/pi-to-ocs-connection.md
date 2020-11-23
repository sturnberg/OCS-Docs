---
uid: piSystemConnection
---

## PI System Connections

### Best Practices for PI System Connections

The most important consideration is to ensure the PI to OCS Agent does not place an excessive load on PI Data Archive. The following recommendations address this issue.

- Only one PI to OCS Agent per connection is allowed to transfer data from a specific PI Data Archive to an OCS namespace. This restriction prevents multiple PI to OCS Agents from pulling data from a single PI Data Archive, which can create an excessive load on the server.
- Install the PI to OCS Agent on a host computer that is separate from your PI Data Archive deployment, so it does not add to the load on the host computer.
- Keep the PI to OCS Agent software version up to date for the best performance. The OCS Portal indicates when an agent is out of date and needs to be updated. 

### Get Started with PI to OCS Connections

To use PI to OCS to transfer data from your PI System to OCS, you must complete the following:

- Create and set up a PI System connection.
- Install the PI to OCS Agent.
- Create a data transfer.

Prerequisite: Before you begin, verify that your organization has a PI System with default PI points (for example, sinusoid) stored on PI Data Archive.

#### Create and Set up a PI System Connection

1.  Click the ![Menu icon](images\menu-icon.png) icon, and then click **Connections** (under Data Management).

    The Connections page opens.

1.  From the **Namespace** drop-down list, click **QuickStart**.

1.  From the **Type** drop-down list, click **PI System**.

1.  Click **Add Connection**.

    The Add PI System Connection window opens.

1.  In the **Name** field, type **QuickStart**. Click **Next.**

1.  On the Review tab, verify that **Source** displays _Not Configured_ and **Destination** displays _QuickStart_. Click **Save**.

The Download Installation Kit window opens. Follow the prompts to download the PI to OCS Agent Installation Kit.

1.  Follow the prompts to download the PI to OCS Agent Installation Kit.

2.  In the Connections page, select the _QuickStart_ connection.

    **Tip:** Click **Manage Permissions** to open the Manage Permissions window. When you are done, click **Cancel**.

    Note: In this window, you only configure permissions on the connection object itself.

    **Tip:** Click **Edit Connection** to open the Edit window.

    Use this window to edit the name and description of the connection. Enter the new name _QuickStartEdit_ and description _PI System Connection used by OCS Quick Start_. Click **Next**. When you are done, click **Save**.

#### Install the PI to OCS Agent

1. In the Details pane on the right side, click **Getting Started Guide** to open the _PI to OCS User Guide_. Follow the installation instructions in the "Install the PI to OCS Agent" topic.

#### Create a data transfer

1.  Once the PI to OCS Agent is installed and registered, return to the Connections page of the OCS portal.
2.  Select the _QuickStart_ connection in the list on the left, and then click **Add PI Point Transfer** in the right pane.
3.  In the Add PI Point Transfer window, in the **Name** field, type _sinusoid_. Click **Search**.
4.  Select the _sinusoid_ PI point from the PI Points Found list, and click **Add**.

    The sinuisoid PI point appears in the PI Points to Transfer list.

5.  Click **Add Transfer** to create the transfer.

    A Data Transfer panel appears in the Details pane. After some time, the **Historical Transfer** field displays 100%, and a new stream with sinusoid data is created in the Sequential Data Store.

6.  To verify the result, open the Sequential Data Store Streams page in OCS
    [here](https://cloud.osisoft.com/data/streams), and look for the sinusoid stream.

7.  Select it, and click **Data** on the tree in the left pane.

    If the PI to OCS Agent has transferred historical data, a value with a recent timestamp will display as the last stream value.

8.  Return to the Connections page.

9.  Select _QuickStartEdit_ in the list, and click **Stop** to end the data transfer.

    Note: Connections cannot be deleted while a transfer is running.
