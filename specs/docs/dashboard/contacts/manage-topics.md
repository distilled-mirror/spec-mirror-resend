> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Topics

> Learn how to create, view, delete, and manage Topics.

[Managing subscribers and unsubscribers](/docs/dashboard/contacts/managing-unsubscribe-list) is a critical part of any email implementation. Topics let your Contacts self-manage their marketing email preferences.

Instead of having a single unsubscribe option for all emails, Topics let your Contacts opt in or out of specific types of communications. This keeps them subscribed to the emails they want to receive.

When you send [Broadcasts](/docs/dashboard/broadcasts/introduction), you can optionally scope [sending with a particular Topic](#send-a-broadcast-with-a-topic). Not only do Topics help you send more precisely, but they also give your users more control over which emails they receive.

## Create a Topic

You can create a new Topic in the [Dashboard](https://resend.com/audience/topics) or programmatically from the [Topics API](/docs/api-reference/topics/create-topic), with a [Topics CLI command](/docs/cli#topics), or with [MCP](/docs/mcp-server).

To create a Topic in the Dashboard:

**1. Go to the **Topics** Dashboard view and click **Create Topic**.**

**2. Enter a name for your Topic.**

Choose something that will help your recipients decide whether they are
interested in receiving these emails, like "announcements" or "product
reviews."

**3. Optionally give your Topic a description.**

**4. Select **Opt-in** or **Opt-out** as the default subscription. This value cannot be changed later.**

<ul>
  <li>
    **Opt-in**: All Contacts will receive the email unless they have
    explicitly unsubscribed from that Topic.
  </li>

  <li>
    **Opt-out**: Subscribers will not receive the email unless they have
    explicitly subscribed to that Topic.
  </li>
</ul>

**5. Select **Public** or **Private** as the visibility.**

<ul>
  <li>
    **Private**: Only Contacts who are opted in to the Topic can see it
    on the unsubscribe page.
  </li>

  <li>
    **Public**: All Contacts can see the Topic on the unsubscribe page.
  </li>
</ul>

![Add Topic](https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-add.png?fit=max\&auto=format\&n=WTZjpSkJsZf7Ubl_\&q=85\&s=0f3f95d5f53d7628b164c04e28e7b4be)

## View all Topics

The [Topics tab of the Audience Dashboard page](https://resend.com/audience/topics) shows you all the Topics you have created along with their details.

![View All Topics](https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-view-all.png?fit=max\&auto=format\&n=WTZjpSkJsZf7Ubl_\&q=85\&s=172afe116b01792855837fc4f987a4be)

You can also [retrieve a single Topic](/docs/api-reference/topics/get-topic) or [list all your Topics](/docs/api-reference/topics/list-topics) via the API or [CLI](/docs/cli#topics).

## Edit Topic details

After creating a Topic, you can edit the following details:

* Name
* Description
* Visibility

To edit a Topic, click the **More options**  button and then **Edit Topic**.

![View edit topic](https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-edit.png?fit=max\&auto=format\&n=WTZjpSkJsZf7Ubl_\&q=85\&s=7f683116ec1dc37aa82c33de94bbd941)

You can also [update a Topic](/docs/api-reference/topics/update-topic) via the API.

> [!NOTE]
>
> You cannot edit the default subscription value after it has been created.

## Delete a Topic

You can delete a Topic by clicking the **More options**  button and then **Remove Topic**.

![Delete Topic](https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-remove.png?fit=max\&auto=format\&n=WTZjpSkJsZf7Ubl_\&q=85\&s=ad5a6bf19aa0f4d858959b91792de167)

You can also [delete a Topic](/docs/api-reference/topics/delete-topic) via the API.

## Send a Broadcast with a Topic

You can send with a Topic in the Broadcast editor from the Topics dropdown menu.

![Send emails with a Topic](https://mintcdn.com/resend/m2xttJpF68pi6Mw0/images/dashboard-broadcast-topics.png?fit=max\&auto=format\&n=m2xttJpF68pi6Mw0\&q=85\&s=95c0a3999269605a66102c15400c5a58)

You can also send with a Topic via the [Broadcast API](/docs/api-reference/broadcasts/create-broadcast).

## Topic Subscription Statuses

When you [view a Contact's details](/docs/dashboard/contacts/manage-contacts#view-contacts), you can see the list of Topics that they are subscribed to.

![Topic Subscription Statuses](https://mintcdn.com/resend/m2xttJpF68pi6Mw0/images/audiences-contacts-topics.png?fit=max\&auto=format\&n=m2xttJpF68pi6Mw0\&q=85\&s=56b25853b46fec447005f7aab32796fa)

You can also check a Contact's subscribed Topics [via the API or SDKs](/docs/api-reference/contacts/get-contact-topics) or with a [Contacts CLI command](/docs/cli#contacts).

## Updating a Topic Subscription for a Contact

When you [create new Topics](#create-a-topic), you can update the subscription preferences of your Contacts to include these Topics. A Contact can belong to multiple Topics, and Resend automatically provides an unsubscribe flow for users who decide to opt out of receiving these emails.

You can add a Contact to a Topic via the Dashboard by expanding the **More options**  and then **Edit Contact**. Add or remove Topics for a given Contact.

![Add Contact to Topic](https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-save-contact-topic.png?fit=max\&auto=format\&n=WTZjpSkJsZf7Ubl_\&q=85\&s=66e212d282f450c371f42a1b214029cd)

You can also update a Topic subscription for a Contact [via the API or SDKs](/docs/api-reference/contacts/update-contact-topics) or with a [Contacts CLI command](/docs/cli#contacts).

## Bulk Subscribe to Topics

You can subscribe multiple Contacts to Topics in the [Dashboard](https://resend.com/audience/) at once:

**1. Go to the **Contacts** Dashboard view.**

**2. Select multiple Contacts by clicking the checkbox next to each Contact.**

**3. Click the **Edit** button in the bulk actions bar.**

**4. Select **Subscribe to Topics****

**5. Choose the Topics you want to subscribe the Contacts to.**

**6. Click **Subscribe****

Learn more about [bulk actions for Contacts](/docs/dashboard/contacts/manage-contacts#bulk-actions).

## API Reference

For complete API documentation, see the [Topics API reference](/docs/api-reference/topics/create-topic).
