> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Contacts

> An introduction to how your Contacts are organized and maintained in Resend.

## Global Contact list

Resend manages a global Contact list for your [Broadcasts](https://resend.com/docs/dashboard/broadcasts/introduction.md) with tools for viewing, organizing, and updating your subscribers.

Contacts are global entities linked to a specific email address. Add additional [Contact properties](#contact-properties), such as a first name, to store additional information and personalize your marketing emails.

Organize your Contacts into [Segments](#segments) for sending Broadcasts, and optionally use [Topics](#topics) to let your Contacts self-manage their receiving preferences.

Each Contact:

* is associated with a single email address
* can have custom properties
* can be in zero, one, or multiple Segments
* can opt in or out of Topics

> [!TIP]
>
> If you previously used our Audience model, learn how to [migrate to the new
> Contacts model](https://resend.com/docs/dashboard/contacts/migrating-from-audiences-to-segments.md).

## Contact features

For each Contact, you can:

* [View and manage](#manage-contacts) individual Contact details.
* Add and update [Contact properties](#contact-properties), including custom properties.
* Assign one or more Broadcast [Segments](#segments) for internal organization.
* Maintain a list of Broadcast [Topics](#topics) they have subscribed to.

![Properties](https://mintcdn.com/resend/2SHIfycCcJlAJEpt/images/audiences-properties-intro.png?fit=max\&auto=format\&n=2SHIfycCcJlAJEpt\&q=85\&s=001cb276f96ad54b6a64042eada0c9c3)

## Quickstart

In the [Dashboard](https://resend.com/audience), add Contacts manually by providing one or more email addresses, or [upload your existing Contacts](https://resend.com/docs/dashboard/contacts/add-contacts.md#add-contacts-by-uploading-a-csv) stored in a `.csv` file.

Add Contacts programmatically with the [Contacts API](https://resend.com/docs/dashboard/contacts/manage-contacts.md#add-contacts-programmatically-via-api) or [CLI commands](https://resend.com/docs/cli.md#contacts).

To add a single Contact manually in the Dashboard:

**1. Navigate to the Audience Dashboard page.**

**2. Select **Add contacts**.**

**3. Select **Add Manually** from the dropdown.**

**4. Add the email address of the Contact in the text field.**

**5. Add the new Contact to an existing Segment.**

> [!NOTE]
>
> An email address is the only required property for a new Contact. However,
> a Contact must belong to a Segment in order to receive a Broadcast.

**6. Confirm and click **Add**.**

See examples of [adding Contacts using other methods](https://resend.com/docs/dashboard/contacts/add-contacts.md).

## Choose your infrastructure

You can build and manage your Contact list entirely from the Resend Dashboard. This allows all members of your team to have full access to your Contact list and to perform any necessary maintenance.

To organize and update your Contacts and their properties from your application, you can use a variety of tools:

* [SDKs](https://resend.com/docs/sdks.md): manage with an SDK built for your language
* [Integrations](https://resend.com/docs/integrations.md): manage with a framework or tool you already use
* [API](https://resend.com/docs/api-reference/contacts/create-contact.md): manage with raw cURL calls
* [CLI](https://resend.com/docs/cli.md#contacts): manage from the terminal
* [MCP server](https://resend.com/docs/mcp-server.md): manage through your agent with MCP

You can also create [Automations](https://resend.com/docs/dashboard/automations/introduction.md) for repeatable actions involving Contacts such as adding new subscribers and updating your Contact list.

See how to use Resend's Contact features such as Segments and Topics in the [Contacts guides](#related-guides).

## Manage Contacts

After you have added Contacts, you'll be able to [view, manage and update Contacts](https://resend.com/docs/dashboard/contacts/manage-contacts.md) and their properties in the [Dashboard page](https://resend.com/audience). This allows all members of your team to maintain your Contact list and to perform any necessary maintenance such as [removing unsubscribed Contacts](https://resend.com/docs/dashboard/contacts/managing-unsubscribe-list.md).

You can also perform these actions programmatically through the [Contacts API](https://resend.com/docs/api-reference/contacts/create-contact.md), [Resend CLI commands](https://resend.com/docs/cli.md#contacts), [Automations](https://resend.com/docs/dashboard/automations/introduction.md), and [MCP server](https://resend.com/docs/mcp-server.md).

Learn more about [managing your Contacts](https://resend.com/docs/dashboard/contacts/manage-contacts.md) in the dedicated guide.

## Contact properties

All Contacts require a valid email address for the `email` property. In order to receive a Broadcast, a Contact will usually also be assigned to a Contact [Segment](#segments).

You can store additional information about your Contacts by adding values for other [Contact properties](https://resend.com/docs/dashboard/contacts/properties.md), including custom defined properties. Contact properties are useful for [personalizing your Broadcasts with dynamic content](https://resend.com/docs/dashboard/contacts/properties.md#use-contact-properties-in-broadcasts), such as greeting recipients by first name.

![Properties](https://mintcdn.com/resend/2SHIfycCcJlAJEpt/images/contact-properties.png?fit=max\&auto=format\&n=2SHIfycCcJlAJEpt\&q=85\&s=6eb917dc7ac58dd515c033cf443e0734)

## Segments

Segments are a tool to group and manage your Contacts for sending Broadcasts. Send Broadcasts to a defined segment of your Contact list to provide extra confidence that you are delivering emails to the intended audience.

**Segments are not visible to your Contacts.** They are only used for your own internal Contact organization. Your Contacts will never see the names of your Segments, and will not know which Segment(s) they belong to.

You can view, add, and manage your Segments in the [Dashboard](https://resend.com/audience) or with any of Resend's programmatic tools such as the [Segments API](https://resend.com/docs/api-reference/segments/create-segment.md), [Resend CLI commands](https://resend.com/docs/cli.md#segments), and [MCP](https://resend.com/docs/mcp-server.md).

You can also create [Automations](https://resend.com/docs/dashboard/automations/introduction.md) to add or remove Contacts from a Segment.

See how to perform common actions to manage your Segments in the dedicated [Segments guide](https://resend.com/docs/dashboard/contacts/manage-segments.md).

## Topics

You can choose to organize your marketing emails into distinct categories based on their subject matter or purpose by assigning a Topic to your Broadcast (e.g., `announcements`, `electronics`). Each Contact has a corresponding `topics` property that determines which Broadcasts they will be sent. If you do not use Topics, then Resend will send your email to every subscribed Contact in the Broadcast's Segment.

Unlike Segments, this optional Contact property can also be updated by subscriber action, and allows your users to self-manage their email preferences.

Scope sending a [Broadcast](https://resend.com/docs/dashboard/broadcasts/introduction.md) to a particular Topic, and subscribers will have the option to unsubscribe from that specific Topic only. This means that your users can continue to receive other emails that are relevant to them. They do not need to unsubscribe from your mailing list entirely.

Resend will handle the unsubscription workflow and update each Contact's list of subscribed Topics in response to user action. You can also manually update this Contact property on the user's behalf, or as part of Automation workflows.

You can view, add, and manage your Topics in the [**Audience** Dashboard](https://resend.com/audience) or with any of Resend's programmatic tools such as the [Topics API](https://resend.com/docs/api-reference/topics/create-topic.md), [Resend CLI commands](https://resend.com/docs/cli.md#topics), and [MCP](https://resend.com/docs/mcp-server.md).

See how to perform common actions to manage your Topics in the dedicated [Topics guide](https://resend.com/docs/dashboard/contacts/manage-topics.md).

## Topics vs Segments

Topics and Segments serve different purposes. They are complementary tools to ensure that your recipients are receiving the emails they want.

| Aspect | Topics | Segments |
| - | - | - |
| **Who controls it** | Your recipients | You (the sender) |
| **Visibility** | Shown on the unsubscribe page | Internal only (recipients never see them) |
| **Purpose** | Let users manage their preferences | Organize Contacts for targeted sending |
| **Example** | "Newsletter," "Product Updates" | "Enterprise customers," "Free trial users" |

## How Segments and Topics work together

Segments are **who you're sending a Broadcast to** and Topics are **what kind of Broadcast you're sending**.

When you send a Broadcast:

1. Choose a **Segment** as your recipients (your sender intent).
2. Label the content with a **Topic** (so the system can respect recipient preferences).
3. Everyone in the Segment receives the message except Contacts who are globally unsubscribed or opted out of that Topic.

For example, you might send a product announcement to your "Enterprise Customers" Segment, labeled with the "Product Updates" Topic. Recipients who previously unsubscribed from product updates are automatically excluded from delivery, even if they are in your "Enterprise Customers" Segment.

**Segments are for targeting. Topics are for protecting preferences.** They work together without competing.

## Related Guides

See how to use Resend's Contact management features.

> [card] [Add Contacts](https://resend.com/docs/dashboard/contacts/add-contacts.md)

> [card] [Manage Contacts](https://resend.com/docs/dashboard/contacts/manage-contacts.md)

> [card] [Contact Properties](https://resend.com/docs/dashboard/contacts/properties.md)

> [card] [Unsubscribe List](https://resend.com/docs/dashboard/contacts/managing-unsubscribe-list.md)

> [card] [Segments](https://resend.com/docs/dashboard/contacts/manage-segments.md)

> [card] [Topics](https://resend.com/docs/dashboard/contacts/manage-topics.md)

## Export your data

Admins can download your data in CSV format for the following resources:

* Emails
* Broadcasts
* Contacts
* Segments
* Domains
* Logs
* API keys

> [!NOTE]
>
> Currently, exports are limited to admin users of your team.

To start, apply filters to your data and click on the "Export" button. Confirm your filters before exporting your data.

<video autoPlay muted loop playsinline src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/exports.mp4?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=1149ee4e83b4414e75a0ecaa92774c38" />

If your exported data includes 1,000 items or less, the export will download immediately. For larger exports, you'll receive an email with a link to download your data.

All admins on your team can securely access the export for 7 days. Unavailable exports are marked as "Expired."

> [!NOTE]
>
> All exports your team creates are listed in the
> [Exports](https://resend.com/exports) page under **Settings** > **Team** >
> **Exports**. Select any export to view its details page. All members of your
> team can view your exports, but only admins can download the data.
