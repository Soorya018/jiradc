---
description: >-
  To create tickets in JIRA Data Center for Squadcast Incidents with the help of Outgoing Webhooks
---

# JIRA Data Center

## Create a Ticket in JIRA DC via Webhook Template

Follow the below steps to configure the “JIRADC - Create Issue” action via webhooks:

1. Copy the **Username** and **Password** of a JIRA DC account that has sufficient permissions to create issues.


## Generate Basic Token using the API Key

You need to generate a basic token using the username and password to authenticate JIRA DC APIs. Use a tool to generate a basic token out of the API Key.

Here we have used [<mark style="color:blue;">Postman</mark>](https://www.postman.com/) to generate the basic token

1. Open a new tab in **Postman**
2. Paste the URL choosing method as POST.  Navigate to **Auth** tab > Select Type as Basic Auth > enter the JIRA account’s **Username** and **Password** in the respective fields.

<div>

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-28 at 18.10.25.png" alt="" width="563"><figcaption></figcaption></figure>

</div>

3. Click on **Code** Icon as highlighted in the below screenshot and copy the **Authorization** value.

## Using Webhooks to create JIRA DC issues for Squadcast Incidents

1. Navigate to **Settings** -> **Webhooks**.
2. Click **Add Webhook**. On the next screen, you will be guided through three steps. Navigate between these steps by clicking on any of the steps on the top bar.
3.  **Add Webhook Details**:&#x20;

    1. **Webhook Name**: Enter the webhook name as **JIRA DC - Create Issue**.
    2. **Webhook Description** (optional): Enter an optional description. For example - This webhook is for issue creation in JIRA DC for Squadcast Incidents.
    3. **Failure Notification Email** (optional): Enter an email where you want to receive failure notifications. This is particularly helpful when you (or an administrator) want to be notified of webhook-related failures.
    4. **URL**: Copy and paste the below API.
    5. **Additional Headers**: Add `Key: Authorization` and paste the `Value` copied from Postman with the prefix **Basic**

    [<mark style="color:blue;">https://<your_JIRA_DC_public_URL>/rest/api/2/issue/</mark>](https://<your_JIRA_DC_public_URL>/rest/api/2/issue)

{% hint style="info" %}
**Note:**

Replace  “**your JIRA DC public URL**” with your **JIRA DC Public URL** and make sure you have selected the **POST** request.

Under Additional headers, Content-Type: application/JSON is added by default.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-28 at 18.14.31.png" alt="" width="563"><figcaption></figcaption></figure>

Click **Next: Choose Webhook Type**, and navigate to the next step.

4. **Choose Webhook Type**: Choose Webhook type (Manual or Automatic) and add configurations.&#x20;
   1. **Manual Webhook**: Manually trigger Webhooks under incidents, on demand. Under Manual Webhook, select the teams that are authorized to access the Webhook. You can select All Teams or enter specific Teams, from the drop-down.

{% hint style="info" %}
<mark style="color:blue;">**Note**</mark>**:**&#x20;

Select this option only if you want to create JIRA DC issues manually on-demand. If you want an issue, created automatically when certain conditions are met, please choose Automatic webhooks.
{% endhint %}

2. **Automatic Webhook**: Automatically trigger Webhooks when the configured conditions match. To set up Automatic Webhook Configurations:
   1. **Versions**: Select **v2**
   2. **Triggers**: Select the following Trigger events (conditions) for which the Webhook will be triggered:
      1. Incident Triggered (This will create a JIRA DC issue whenever a new incident gets triggered in Squadcast)
   3. **Filters**: You can apply filters on top of events, based on Teams, Services, Alert Sources, and Tags, by having an individual expression or a combination of expressions/expression groups.&#x20;

Applying filters will trigger the webhook and create JIRA DC issues only for events that match the filter.

<figure><img src="../../.gitbook/assets/Screenshot 2023-04-28 at 18.14.39 (1).png" alt="" width="563"><figcaption></figcaption></figure>

Click **Next: Configure Payload**, and navigate to the next step.

5. **Configure Payload**:\
   \
   Select the pre-configured template for **JIRA DC - Create Issue**. You can also test the Webhook by clicking the **Test Webhook** on the bottom right.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-08 at 11.41.06.png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:**

We have added the necessary fields in the template. You can change the **Priority** and **Status** according to your use case and can add additional ticket fields. You can also [use this link](https://developer.atlassian.com/server/jira/platform/jira-rest-api-examples/) to check the fields accepted by JIRA DC Create Issue API.
{% endhint %}

Click **Save** and your **Webhook** is created.
