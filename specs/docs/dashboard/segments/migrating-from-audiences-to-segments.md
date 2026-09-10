> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrating from Audiences to Segments

> Learn how to migrate from Audiences to Segments

Contact segmentation at Resend has changed to simplify managing your contacts. Before, each Contact was part of one Audience and if you created another contact with the same email address in a different Audience, it would be a completely separate object.

In the new model, Contacts are now independent of Audiences, which are now called Segments. A Contact can be in zero, one or multiple Segments and still count as one when calculating your quota usage.

Contacts API endpoints that previously required an `audience_id` can now be used directly instead.

## What's changing

Resend now uses a **Global Contacts** model.

* **Before**: If a Contact with the same email appeared in multiple Segments, it was counted as multiple Contacts.
* **Now**: Each email address is treated as a single Contact across your team, even if it appears in multiple Segments.

The new model offers three concepts:

* **Contact**: a global entity linked to a specific email address.
* **Segment**: an internal segmentation tool for your team to organize sending.
* **Topic**: a user-facing tool for managing email preferences.

## Unsubscribing

Previously, when a contact clicked "unsubscribe," their contact status were marked was "Unsubscribed" only from the specific Audience used in that Broadcast.

From now on, contacts will see a preference page where they can:

* Unsubscribe from certain **Topics** (email's preference).
* Or unsubscribe from **everything** you send (update contact status).

## What to Do

If you've been using Audiences for both segmentation and unsubscribes, switch your unsubscribe logic to **Topics**:

1. Create a Topic for each type of email you send.
2. Assign the right users to each Topic.
3. Use Segments purely for your internal organization.

With this setup, when you send a Broadcast, your users can choose which Topics to unsubscribe from, or opt out completely.

For details on the new API endpoints view:

* [Contacts](/docs/api-reference/contacts/create-contact)
* [Topics](/docs/api-reference/topics/create-topic)
* [Segments](/docs/api-reference/segments/create-segment)

## Get more help

If you have a use case not covered here, [please reach out](https://resend.com/help) for a smooth transition.
