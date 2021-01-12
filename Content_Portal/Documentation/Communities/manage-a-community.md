---
uid: ManageCommunity
---

# Manage tenants in a community

The Community Details page lets you perform various tasks for managing tenants belonging to a community.

To create a new community, see [Add a community](xref:AddCommunity).

## Add a tenant to a community

OCS lets you invite business partners to join a community so they are enabled to share data. The business partner must already be a tenant in OCS.

Two different users must perform this procedure:

- One user, the "inviter," issues an invitation to another tenant to join a community.
- Another user in separate tenant, the "invitee," accepts the invitation.

**Note.** Only an OCS user whose role is Community Administrator, Community Moderator, or Tenant Administrator can be an inviter. Only an OCS user whose role is a Tenant Administrator or Community Administrator can be an invitee.  

1. **Inviter:** Perform the following steps:   
   1.1. On the Communities overview page, find the community you want to share and click **Details**.   
   1.2. On the Community Details page, on the Tenant card, click **New Tenant**.   
   1.3. Enter the email address of the representative of the tenant you would like to invite and click **Invite**. An email is sent to the invitee.
2. **Invitee:** Perform the following steps:   
   2.1 Open the email from OSIsoft Cloud Services and click **VIEW COMMUNITY INVITE**. OCS opens and displays a login dialog.   
   2.2. Enter the name of your tenant and click **Continue**. A dialog for verifying identity appears.   
   2.3. Verify your identity. OCS displays a page saying that your tenant will be joining the community from which the invite was issued.   
   2.4. Click **Join**. The inviter receives an email asking for confirmation of the pending invitation.   
3. **Inviter:** Perform the following steps:   
   3.1. Click **VIEW PENDING INVITATIONS**. After authentication into OCS, the Community Details page opens and shows that an invitation awaits confirmation.   
   3.2. Select the tenant with the pending confirmation, select **More Options** ![More Options](..\images\more-options-wite-background.png "More Options"), and click **Confirm Tenant**. When prompted for confirmation, click **Confirm Tenant** again.

## Pause or resume sharing data

## Remove a tenant from a community

Use this procedure to remove a tenant from a community. This action might be necessary if a business relationship changes or a security breach occurs.

After removing a tenant, you can re-invite the tenant to the community but all data that was previously shared must be shared again with the returning tenant.

**Note.** Only an OCS user whose role is Community Administrator, Community Moderator, or Tenant Administrator can remove a tenant from a community. ???waiting to see API to confirm permissions???  

1. On the Communities overview page, find the community you want to modify and click **Details**.
2. On the Community Details page, select the tenant you want to remove from the community.
3. select **More Options** ![More Options](..\images\more-options-wite-background.png "More Options") and click **Remove Tenant**. When prompted for confirmation, click **Remove Tenant** again.

## Remove your own tenant from a community

Use this procedure to remove your own tenant from a community.

After removing you tenant, you can be re-invited to the community but all data that was previously shared with your tenant must be shared again.

**Note.** Only an OCS user whose role is Community Administrator, Community Moderator, or Tenant Administrator can remove a tenant from a community. ???waiting to see API to confirm permissions???  

1. On the Communities overview page, find the community you want to leave and click **Details**.
2. On the Community Details page, select the tenant you want to remove from the community.
3. select **More Options** ![More Options](..\images\more-options-wite-background.png "More Options") and click **Remove Tenant**. When prompted for confirmation, click **Remove Tenant** again.