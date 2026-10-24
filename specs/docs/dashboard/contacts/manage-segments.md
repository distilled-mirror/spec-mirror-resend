> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Managing Segments

> Learn how to create, retrieve, and delete Segments.

Segments are used to organize your [Contacts](https://resend.com/docs/dashboard/contacts/introduction.md) into groups for sending [Broadcasts](https://resend.com/docs/dashboard/broadcasts/introduction.md). **Segments are not visible to your Contacts.** They are only used for your own internal Contact management.

## Create Segments

You can create Segments in the [Dashboard](https://resend.com/audience/segments), or programmatically from the [Segments API](https://resend.com/docs/api-reference/segments/create-segment.md), with a [Segments CLI command](https://resend.com/docs/cli.md#segments), or [MCP](https://resend.com/docs/mcp-server.md).

To create a Segment in the Resend Dashboard:

**1. Go to the **Segments** Dashboard view.**

**2. Select **Create Segment**.**

**3. Enter a name.**

Enter a name for your Segment that describes the Contacts in this group
(e.g., "newsletter subscribers", "free trial users").

**4. Click **Add** to confirm.**

## View Segments

The [**Segments** Dashboard view](https://resend.com/audience/segments) shows a list of all Segments in your account, when they were created, and how many Contacts are in each Segment.

## Edit Segments

Click the **More options**  menu next to each Segment to:

* edit the Segment name
* copy the Segment ID to your clipboard
* delete the Segment

Click on any Segment to view the list of Contacts that belong to that Segment.

You can also retrieve a single Segment, list of Segments, or the list of Contacts in a Segment, from the [Segments API](https://resend.com/docs/api-reference/segments/get-segment.md), with a [Segments CLI command](https://resend.com/docs/cli.md#segments), or [MCP](https://resend.com/docs/mcp-server.md).

## Updating the Segments of a Contact

A Contact can belong to multiple Segments. Because Segments are only used to organize your Contacts internally for sending Broadcasts, you do not need consent to add a user to a Segment.

You can add a Contact to a Segment via the Dashboard by [editing the Contact](https://resend.com/docs/dashboard/contacts/manage-contacts.md#edit-contacts) and choosing to add or remove Segments.

You can also use the [Contacts API](https://resend.com/docs/api-reference/contacts/add-contact-to-segment.md) or [Contacts CLI commands](https://resend.com/docs/cli.md#contacts) to add or remove Segments from a Contact's profile programmatically.

> [!NOTE]
>
> If a Contact's unsubscribed status is `true`, or the Contact is on the [Suppression List](https://resend.com/docs/dashboard/emails/email-suppressions.md), Resend will not send any emails to them, even if you have added them to a Segment.
>
> Regularly [review your unsubscribe list](https://resend.com/docs/dashboard/contacts/managing-unsubscribe-list.md) and remove recipients from your Contact list who no longer wish to receive your emails.

## Delete Segments

When you delete a Segment, no Contacts are deleted. The Segment is removed from your list, and from the `segments` property of all associated Contacts.

You can delete Segments in the [Dashboard](https://resend.com/audience/segments), or programmatically from the [Segments API](https://resend.com/docs/api-reference/segments/delete-segment.md), with a [Segments CLI command](https://resend.com/docs/cli.md#segments), or with [MCP](https://resend.com/docs/mcp-server.md).

To delete one or more Segments in the Dashboard:

**1. Go to the **Segments** Dashboard view.**

**2. Select the Segment(s) you want to delete by clicking the checkboxes next to each Segment.**

**3. Click **Delete** in the bottom action bar.**

**4. Type the Segment name (for single selection) or `DELETE N SEGMENTS` (for multiple) to confirm.**

**5. Press **Cmd+Enter** or click **Delete Segments** to complete.**

You can also use keyboard shortcuts:

* **Cmd+A** to select all Segments on the current page.
* **Backspace** to open the delete confirmation modal.

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

## API Reference

For complete API documentation, see the [Segments API reference](https://resend.com/docs/api-reference/segments/create-segment.md).
