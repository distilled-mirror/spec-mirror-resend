> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Topics

> Give your users more control over their subscription preferences.

Managing subscribers and unsubscribers is a critical part of any email implementation. Topics are used by your contacts to manage their email preferences.

When you send [Broadcasts](/docs/dashboard/broadcasts/introduction), you can optionally scope sending to a particular Topic. Not only does scoping your sending help you send more precisely, but it also allows your users to manage their preferences with more control.

<Tip>
  New to Topics? Learn [why and when to use
  them](/docs/knowledge-base/why-use-topics), including how they improve
  deliverability and differ from Segments.
</Tip>

## Add a Topic

You can create a new Topic from the [dashboard](https://resend.com/audience/topics) or [via the API](/docs/api-reference/topics/create-topic).

1. Click **Create Topic**.
2. Give your Topic a name.
3. Give your Topic a description (optional).
4. Select **Opt-in** or **Opt-out** as the default subscription. This value **cannot** be changed later.
   * **Opt-in**: all Contacts will receive the email unless they have explicitly unsubscribed from that Topic.
   * **Opt-out**: subscribers will not receive the email unless they have explicitly subscribed to that Topic.
5. Select **Public** or **Private** as the visibility.
   * **Private**: only Contacts who are opted in to the Topic can see it on the unsubscribe page.
   * **Public**: all Contacts can see the Topic on the unsubscribe page.

<img alt="Add Topic" src="https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-add.png?fit=max&auto=format&n=WTZjpSkJsZf7Ubl_&q=85&s=0f3f95d5f53d7628b164c04e28e7b4be" height={450} width={720} data-path="images/dashboard-topics-add.png" />

## View all Topics

The [dashboard](https://resend.com/audience/topics) shows you all the Topics you have created along with their details.

<img alt="View All Topics" src="https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-view-all.png?fit=max&auto=format&n=WTZjpSkJsZf7Ubl_&q=85&s=172afe116b01792855837fc4f987a4be" width="1800" height="923" data-path="images/dashboard-topics-view-all.png" />

You can also [retrieve a single Topic](/docs/api-reference/topics/get-topic) or [list all your Topics](/docs/api-reference/topics/list-topics) via the API.

## Edit Topic details

After creating a Topic, you can edit the following details:

* Name
* Description
* Visibility

To edit a Topic, click the **More options** <Icon icon="ellipsis" iconType="solid" /> button and then **Edit Topic**.

<img alt="View edit topic" src="https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-edit.png?fit=max&auto=format&n=WTZjpSkJsZf7Ubl_&q=85&s=7f683116ec1dc37aa82c33de94bbd941" width="1800" height="923" data-path="images/dashboard-topics-edit.png" />

You can also [update a Topic](/docs/api-reference/topics/update-topic) via the API.

<Info>
  You cannot edit the default subscription value after it has been created.
</Info>

## Delete a Topic

You can delete a Topic by clicking the **More options** <Icon icon="ellipsis" iconType="solid" /> button and then **Remove Topic**.

<img alt="Delete Topic" src="https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-topics-remove.png?fit=max&auto=format&n=WTZjpSkJsZf7Ubl_&q=85&s=ad5a6bf19aa0f4d858959b91792de167" width="1800" height="923" data-path="images/dashboard-topics-remove.png" />

You can also [delete a Topic](/docs/api-reference/topics/delete-topic) via the API.

## Editing Topics for a Contact

As you receive [proper consent to email Contacts](/docs/knowledge-base/what-counts-as-email-consent), add the Contact to a given Topic. A Contact can belong to multiple Topics.

You can add a Contact to a Topic via the dashboard by expanding the **More options** <Icon icon="ellipsis" iconType="solid" /> and then **Edit Contact**. Add or remove Topics for a given Contact.

<img alt="Add Contact to Topic" src="https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-save-contact-topic.png?fit=max&auto=format&n=WTZjpSkJsZf7Ubl_&q=85&s=66e212d282f450c371f42a1b214029cd" width="1800" height="923" data-path="images/dashboard-save-contact-topic.png" />

<Note>
  The **Subscribed** status is a global setting that enables or disables sending to a Contact for Broadcasts.

  * If a Contact's **Subscribed** status is
    **false**, they will not receive emails from your account, even if they have
    opted-in to a specific Topic.

  * If the **Subscribed** status is **true**, they
    can receive emails from your account.

  Learn more about [managing your unsubscribe list](/docs/dashboard/audiences/managing-unsubscribe-list).
</Note>

## Sending Broadcast with a Topic

You can send with a Topic in the Broadcast editor from the Topics dropdown menu.

<img src="https://mintcdn.com/resend/m2xttJpF68pi6Mw0/images/dashboard-broadcast-topics.png?fit=max&auto=format&n=m2xttJpF68pi6Mw0&q=85&s=95c0a3999269605a66102c15400c5a58" alt="Send emails with a Topic" width="1772" height="688" data-path="images/dashboard-broadcast-topics.png" />

You can also send with a Topic via the [Broadcast API](/docs/api-reference/broadcasts/create-broadcast).

## Unsubscribing from a Topic

If a Contact clicks a Broadcast unsubscribe link, they will see a preference page where they can:

* Unsubscribe from certain **Topics** (types of email)
* Or unsubscribe from **everything** you send

If they unsubscribe from a Topic or several Topics, they will no longer receive emails for those Topics. If they unsubscribe from all emails from your account, Broadcasts will no longer send to them.

You can [customize your unsubscribe page with your branding](/docs/dashboard/settings/unsubscribe-page) from your team settings.

<img src="https://mintcdn.com/resend/WTZjpSkJsZf7Ubl_/images/dashboard-unsubscribe-page-topics.png?fit=max&auto=format&n=WTZjpSkJsZf7Ubl_&q=85&s=11896d54a3e2bdb510a5b666ae7ee8a8" alt="See Topics on the Unsubscribe Page" width="1800" height="923" data-path="images/dashboard-unsubscribe-page-topics.png" />
