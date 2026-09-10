> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage Broadcasts

> Learn how to view, update, and delete your Broadcasts.

After you create your first Broadcast, all members of your team can view and manage existing Broadcast details directly in the [**Broadcasts** Dashboard page](https://resend.com/broadcasts). You can also perform bulk actions (cancel, delete) by selecting multiple Broadcasts.

To manage your marketing campaigns directly from your application, you can use the [Broadcast API](/docs/api-reference/broadcasts/create-broadcast) endpoints to list, retrieve, update, and delete your existing Broadcasts.

You can also manage your Broadcasts using [Resend CLI commands](/docs/cli#broadcasts) and [AI building tools](/docs/ai-onboarding).

## View Broadcasts

See the name, [status](#understand-broadcast-statuses), and created date of all your Broadcasts from the Emails Dashboard page. These can also be filtered by status and [audience](/docs/dashboard/segments/introduction).

Select any individual Broadcast to view its details. The view will depend on the status of the email. For example, Broadcasts that have been sent will show deliverability metrics as well as your content as a preview, plain text, and HTML.

Clicking on a draft Broadcast will bring up the Dashboard editor for further editing.

## Understand Broadcast statuses

Here are all the statuses that can be associated with a Broadcast:

* `draft`: The Broadcast is a draft. Drafts can be edited, deleted, or scheduled for sending.
* `scheduled`: The Broadcast is scheduled to be sent at a specific time. Scheduled Broadcasts can have their schedule canceled, which returns them to draft status and prevents any emails from being sent.
* `sent`: The Broadcast was sent.
* `queued`: The Broadcast is queued for delivery. Canceling a queued Broadcast stops delivery to the remaining recipients only. Emails already sent cannot be recalled.
* `canceled`: The Broadcast was canceled while it was queued for delivery. It cannot be sent again.

## Edit Broadcasts

You can edit the content and properties of any draft or scheduled Broadcast. Once a Broadcast has been sent, only its name can be updated.

To edit an existing draft or scheduled Broadcast in the Dashboard:

1. Click the name of the Broadcast you want to edit.
2. Use the Dashboard editor to update any properties or content.
3. Exit the editor when you have finished editing. Your changes will be automatically saved.

## Cancel scheduled Broadcasts

Canceling a Broadcast only stops emails that haven't been sent yet. Any emails already delivered cannot be recalled. If a Broadcast is mid-send (`queued`), canceling halts delivery to the remaining recipients.

To cancel the schedule for one or more scheduled Broadcasts in the Dashboard:

1. Select the scheduled Broadcast(s) you want to cancel.
2. Click **Cancel schedule** in the bottom action bar.
3. Type `CANCEL` to confirm.
4. Press **Cmd+Enter** or click **Cancel schedules** to complete.

When you cancel a scheduled Broadcast, it returns to draft status and won't be sent at the scheduled time. When you cancel a Broadcast that is mid-send (`queued`), it is set to the `canceled` status and cannot be sent again.

## Delete draft Broadcasts

Only draft (including scheduled) Broadcasts can be deleted. Once a Broadcast has been sent or queued, it can't be deleted.

To delete one or more draft Broadcasts in the Dashboard:

1. Select the Broadcast(s) you want to delete by clicking the checkboxes next to each Broadcast.
2. Click **Delete** in the bottom action bar.
3. Type the Broadcast name (for single selection) or `DELETE N BROADCASTS` (for multiple) to confirm.
4. Press **Cmd+Enter** or click **Delete Broadcasts** to complete.

You can also use keyboard shortcuts:

* **Cmd+A** to select all Broadcasts on the current page
* **Backspace** to open the delete confirmation modal

## API Reference

For complete API documentation, see the [Broadcasts API reference](/docs/api-reference/broadcasts/create-broadcast).
