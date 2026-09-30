> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Migrating from Audiences to Segments

> Learn how to migrate from Audiences to Segments

In November 2025, [Resend changed how Contacts are segmented](https://resend.com/blog/new-contacts-experience#segmenting-contacts). Before, each Contact was part of one Audience and if you created another Contact with the same email address in a different Audience, it would be a completely separate object.

Contacts are now independent of the groups they belong to, and the former Audiences are now called Segments. A Contact can be in zero, one or multiple Segments and count as only one Contact toward your Contact quota.

Contacts API endpoints that previously required an `audience_id` can now be used directly instead. The [Audiences API](https://resend.com/docs/api-reference/audiences/create-audience) is now deprecated and will be removed in the future.

## What changed

Resend now uses a **Global Contacts** model.

* **Before**: If a Contact with the same email appeared in multiple Segments, it was counted as multiple Contacts.
* **Now**: Each email address is treated as a single Contact across your team, even if it appears in multiple Segments.

The [current Contact model](/docs/dashboard/contacts/introduction) includes four concepts:

* **Contact**: a global entity linked to a specific email address.
* **Segment**: an internal segmentation tool for your team to organize sending.
* **Topic**: a user-facing tool for managing email preferences.
* **Contact properties**: a set of key-value pairs that can be used to store additional information about a Contact.

## Unsubscribing

Previously, when a Contact clicked "unsubscribe," their Contact status was marked as "Unsubscribed" only from the specific Audience used in that Broadcast.

Now, Contacts will see a preference page where they can:

* Unsubscribe from certain **Topics** (email's preference).
* Or unsubscribe from **everything** you send (update Contact status).

## What you should do

If you've been using Audiences for both segmentation and unsubscribes, we recommend switching your unsubscribe logic to **Topics**:

1. Create a Topic for each type of email you send.
2. Assign the right users to each Topic.
3. Use Segments purely for your internal organization.

With this setup, when you send a Broadcast, your users can choose which Topics to unsubscribe from, or opt out completely.

For details on the new API endpoints view:

* [Contacts](/docs/api-reference/contacts/create-contact)
* [Topics](/docs/api-reference/topics/create-topic)
* [Segments](/docs/api-reference/segments/create-segment)

## Additional Help

If you have a use case not covered here, [please reach out](https://resend.com/help) for assistance and a smooth transition.
