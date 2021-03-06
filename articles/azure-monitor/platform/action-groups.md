---
title: Create and manage action groups in the Azure portal
description: Learn how to create and manage action groups in the Azure portal.
author: dkamstra
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 11/30/2018
ms.author: dukek
ms.component: alerts
---
# Create and manage action groups in the Azure portal
## Overview ##
An action group is a collection of notification preferences defined by the owner of an Azure subscription. Azure Monitor and Service Health alerts use action groups to notify users that an alert has been triggered. Various alerts may use the same action group or different action groups depending on the user's requirements.

When an action is configured to notify a person by email or SMS the person will receive a confirmation indicating he / she has been added to the action group.

This article shows you how to create and manage action groups in the Azure portal.

Each action is made up of the following properties:

* **Name**: A unique identifier within the action group.  
* **Action type**: The action to perform. Examples include sending a voice call, SMS, email; or triggering various types of automated actions. See types later in this article. 
* **Details**: The corresponding details which vary by *action type*. 

For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](../../azure-monitor/platform/action-groups-create-resource-manager-template.md).

## Create an action group by using the Azure portal ##
1. In the [portal](https://portal.azure.com), select **Monitor**. The **Monitor** blade consolidates all your monitoring settings and data in one view.

    ![The "Monitor" service](./media/action-groups/home-monitor.png)
1. Select **Alerts** then select **Manage action groups**.

    ![Manage Action Groups button](./media/action-groups/manage-action-groups.png)
1. Select **Add action group**, and fill in the fields.

    ![The "Add action group" command](./media/action-groups/add-action-group.png)
1. Enter a name in the **Action group name** box, and enter a name in the **Short name** box. The short name is used in place of a full action group name when notifications are sent using this group.

      ![The Add action group" dialog box](./media/action-groups/action-group-define.png)

1. The **Subscription** box autofills with your current subscription. This subscription is the one in which the action group is saved.

1. Select the **Resource group** in which the action group is saved.

1. Define a list of actions by providing each action's:

    a. **Name**: Enter a unique identifier for this action.

    b. **Action Type**: Select Email/SMS/Push/Voice, Logic App, Webhook, ITSM, or Automation Runbook.

    c. **Details**: Based on the action type, enter a phone number, email address, webhook URI, Azure app, ITSM connection, or Automation runbook. For ITSM Action, additionally specify **Work Item** and other fields your ITSM tool requires.

1. Select **OK** to create the action group.

## Manage your action groups ##
After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade. Select the action group you want to manage to:

* Add, edit, or remove actions.
* Delete the action group.

## Action specific information
**Azure app Push** - You may have up to 10 Azure app actions in an Action Group. At this time the Azure app action only supports ServiceHealth alerts. Any other alert time will be ignored. See [configure alerts whenever a service health notification is posted](../../azure-monitor/platform/alerts-activity-log-service-notifications.md).

**Email** - Emails will be sent from the following email addresses. Ensure that your email filtering is configured appropriately
   - azure-noreply@microsoft.com
   - azureemail-noreply@microsoft.com
   - alerts-noreply@mail.windowsazure.com

You may have up to 1000 email actions in an Action Group. See the [rate limiting information](./../../azure-monitor/platform/alerts-rate-limiting.md) article

**ITSM** - You may have up to 10 ITSM actions in an Action Group
ITSM Action requires an ITSM Connection. Learn how to create an [ITSM Connection](../../azure-monitor/platform/itsmc-overview.md).

**Logic App** - You may have up to 10 Logic App actions in an Action Group

**Function App** - The function keys for Function Apps configured as actions are read through the Functions API, which currently requires v2 function apps to configure the app setting “AzureWebJobsSecretStorageType” to “files”, see [Changes to Key Management in Functions V2]( https://aka.ms/funcsecrets) for more information.

**Runbook** - You may have up to 10 Runbook actions in an Action Group
Refer to the [Azure subscription service limits](../../azure-subscription-service-limits.md) for limits on Runbook payloads

**SMS** - You may have up to 10 SMS actions in an Action Group
See the [rate limiting information](./../../azure-monitor/platform/alerts-rate-limiting.md) article
See the [SMS alert behavior](../../azure-monitor/platform/alerts-sms-behavior.md) article

**Voice** - You may have up to 10 Voice actions in an Action Group</dd>
See the [rate limiting information](./../../azure-monitor/platform/alerts-rate-limiting.md) article</dd>

**Webhook** - You may have up to 10 Webhook actions in an Action Group. 
Retry logic - The timeout period for a response is 10 seconds. The webhook call will be retried a maximum of 2 times when the following HTTP status codes are returned: 408, 429, 503, 504 or the HTTP endpoint does not respond. The first retry happens after 10 seconds. The second and last retry happens after 100 seconds.

Source IP address ranges
    - 13.106.57.181
    - 13.106.54.3
    - 13.106.54.19
    - 13.106.38.142
    - 13.106.38.148
    - 13.106.57.196

To receive updates about changes to these IP addresses we recommend you configure a [Service Health alert](./../../azure-monitor/platform/service-notifications.md) which monitors for Informational notifications about the Action Groups service.


## Next steps ##
* Learn more about [SMS alert behavior](../../azure-monitor/platform/alerts-sms-behavior.md).  
* Gain an [understanding of the activity log alert webhook schema](../../azure-monitor/platform/activity-log-alerts-webhook.md).  
* Learn more about [ITSM Connector](../../azure-monitor/platform/itsmc-overview.md)
* Learn more about [rate limiting](../../azure-monitor/platform/alerts-rate-limiting.md) on alerts.
* Get an [overview of activity log alerts](../../azure-monitor/platform/alerts-overview.md), and learn how to receive alerts.  
* Learn how to [configure alerts whenever a service health notification is posted](../../azure-monitor/platform/alerts-activity-log-service-notifications.md).
