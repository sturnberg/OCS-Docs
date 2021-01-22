---
uid: GSNamespaces
---

# Namespaces

A namespace is a logical unit of organization for data within a tenant. Each tenant may contain more than one namespace. Before any data can be put into OCS for a given tenant, a namespace must be created within the scope of that tenant. When a namespace is created, the region where that namespace will reside (for example, West US) needs to be specified. Once the namespace is created and the necessary resources allocated to support it, any data put into the namespace will reside in the selected region.

When a namespace is created, a set of OSIsoft Cloud Services (OCS) data processing resources (for example, SDS and Asset service), along with the associated storage resources, are allocated to support that namespace. Each namespace is distinct and separate from other namespaces and, therefore, they isolate the resources contained within it. The resources are scoped to the namespace. Therefore, you can create an SdsType or an SdsStream object with the same name in two different namespaces.

Any data stored within a namespace is tied to that namespace, along with the region where the namespace was allocated. OCS does not currently provide a mechanism to directly transfer data from one namespace (or region) to any other namespace (or region). To migrate data between namespaces, and thus between namespaces in different regions, the data must be exported from the source namespace in OCS, then imported into the destination namespace.

## PI Core Counterpart

In PI Core Services, a namespace is similar to a full PI Server. Much like a PI Server, a namespace has its own resources and it is not typical or easy to use data from multiple namespaces at the same time. It is reasonable for an account to use only one namespace.

## Namespace IDs

The namespace ID must be unique across the tenant.

The namespace ID must meet these requirements:

- Contain 100 or fewer characters
- Can include alphanumeric characters, underscores (\_), dashes (-), spaces, and periods
- Cannot contain two consecutive periods or two consecutive underscores
- Cannot begin or end with a period
- Cannot start with two consecutive underscores <!-- LA: need to verify this with engineering -->
- Cannot include leading or trailing white spaces

## Querying Data Across Namespaces

When querying API endpoints, the namespace ID is part of the URL. The API URL takes the form `https://{server}/api/{version}/Tenants/{tenant id}/Namespaces/{namespace id}`, followed by the API path, such as `/Streams`. Because the namespace is included in the URL, it is not possible to make a single API request for data across multiple namespaces.

## Namespace Best Practices

OSIsoft recommends using one of the following strategies when creating namespaces:

- Use Case 1 -- Create a separate namespace for each environment, for example, Production, Development, Staging, and so on.
- Use Case 2 -- Create a separate namespace for each end-user customer.

The first strategy is recommended for accounts where all the data belongs to one organization. Generally, it is not good practice to create separate namespaces for data that will later need to be used together.  

The second strategy may be preferable if you are providing a service to multiple end-user customers that use OSIsoft Cloud Services as a backend. This strategy makes it easier to avoid naming conflicts for end-users. It can also make it easier to manage security and assign permissions. However, it is important to note that security on a namespace is not automatically inherited by the objects and collections within it. If your organization has internal data that does not belong to an end-user customer, you may want to consider combining both strategies. Create separate namespaces for each customer and one namespace for internal use that includes your Production, Development, and Staging environments.

## Get Started with Namespaces

Creating a namespace is a resource-intensive operation. Therefore, you may prefer to use an existing namespace. In this procedure, the ID assigned to the namespace is QuickStart. Throughout the Getting Started, we will refer to the namespace with this name. Substitute "QuickStart" with the name of an existing namespace or any other name you prefer.

1. Click the ![Menu icon](images\menu-icon.png) icon and click **Namespaces** (under Data Management).


2. In the Manage Namespaces pane, click **Add Namespace**. 

3. In the Namespace Id field, enter _QuickStart_ for your namespace ID, enter a description, and select a region. 

   Note: Once the namespace is created, the **Namespace Id** and **Region** cannot be changed.

   When you are done, click **Add**.

4. Click **Display Details**.  

   - The window shows your account ID, namespace ID, description, and region of your namespace. It also displays zero (0) in the **Type Count** and **Stream Count** fields.  
   - The details window shows the **State**, which indicates the status of the namespace. Once the process of creating a namespace and bringing it online is complete, the **State** changes to **Active**. If the status is not yet **Active**, close the window and refresh the page. 

    Note: It will take some time for the namespace to be created. 

   <!-- LA: What is the status while the namespace is being set up? Can we give them an estimate of how long it might take for the namespace status to change to Active? Follow up with Derek. -->

5. Select the namespace in the list, and click **Edit Namespace**.  

   Note: The only field you can edit is the **Description** field.

6. Make any changes to the description and click **Save**.

#### How to manage permissions on the namespace

<!-- DB: I think it makes sense to have that discussion as part of the Roles discussion, since that's the explicit purpose of Roles. But agreed it shouldn't be repeated in every page. --><!-- LA: I will make a pass through all the topics once we've created the Roles topic. -->

Access control is managed by assigning permissions to roles. Each role is granted (**Allow**) or denied (**Deny**) permission to perform an access operation (read, write, delete, or manage permissions). Users are assigned to a role that determines their access to OCS resources. 

Note: The remaining steps are optional. 

1. Click **Manage Permissions**.
2. Click the **Selected role** arrow, and select Account Member from the list.
3. Give the account member write permissions by selecting the **Allow** checkbox for the **Write** access type.
4. Click **Save**.
