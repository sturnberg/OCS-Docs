---
uid: omfConnection
---

## OSIsoft Messaging Format Connection

### Best Practices for OMF Connections

The most important considerations with OMF connections are to ensure applications use the correct client credentials and security is correctly configured for OMF connections.

- Each type of application or system that sends OMF data to OCS should have its own defined OMF connection, with the name and description referencing the data source.
- Each application instance or each device that sends OSIsoft Message Format (OMF) data to OCS should have its own client credentials client and its own secret. Connections allow a list of clients to be defined. When each application instance or device has its own client, security is improved because secrets can be managed at a granular level.
- Ensure that the client credentials client has the minimum roles and access in OCS. For example, a client may be granted access to write data, but it does not have permissions to delete data.
- For use cases that involve a large number of source applications or source devices, the OCS API can be used to automatically assign a new client credentials client and secret whenever a new device is brought online.

### Get Started with OMF Connections

To send OMF data to OCS, you must first configure an OMF connection. Use this getting started procedure to become familiar with OMF connections.

1. Click the ![Menu icon](images\menu-icon.png) icon and click **Clients** (below Security) to open the Manage Clients page.

2. Verify that there is at least one client credentials client to use in the OMF connection. If you need to create one, refer to the Clients section.

1.  Click on the menu and click **Connections** (under Data Management).

2.  From the **Namespace** field, select _QuickStart_.

3.  From the **Type** drop-down list, select **OMF**.

4.  Click **Add Connection** to open the Add PI System Connection window.

5.  In the **Name** field, enter _QuickStart_ and click **Next**.

6.  In the Clients tab, click one of the clients in the Available list to add it
    to the Selected List. Click **Next**.

    Note: For the purposes of this Getting Started exercise, you may choose any client.

7.  In the Namespaces tab, verify that the QuickStart namespace appears in the
    Selected list. Click **Next**.

8.  In the Review tab, verify that the Clients list shows the client credentials
    client you chose, and the Namespace list shows the QuickStart namespace.
    Click **Save**.

    An application can now use the selected client credentials client to write OMF data to the QuickStart namespace.

11. Follow these tips to learn more about OMF connections.

     **Tip:** Click **Manage Permissions** to open the Manage Permissions window.

     Note: In this window, you configure permissions only on the connection object itself. Click **Cancel** to continue.

     **Tip:** Click **Edit Connection** to open the Edit window.

     Use this window to edit the name and description of the connection. Enter the new name _QuickStartEdit_ and enter the description _OMF Connection used by OCS Quick Start_. Click **Next**, and then click **Save** when you are done.
