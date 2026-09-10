> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to cancel a Broadcast

> Cancel a scheduled Broadcast or stop one that is still sending.

You can cancel a Broadcast that is scheduled or still sending. When you cancel a Broadcast, here's what happens based on its status:

* `scheduled` → `draft`: no emails are sent. You can update the Broadcast and reschedule it to be sent.
* `queued` → `canceled`: emails that have already been sent are not affected, but any emails still in the queue will no longer be sent.

## Cancel a Broadcast

1. Go to [Broadcasts](https://resend.com/broadcasts) and open the scheduled or sending Broadcast.
2. Click **Cancel** on the Broadcast page.

Resend then returns a scheduled Broadcast to `draft`, or halts delivery to the remaining recipients if the Broadcast is sending.

You can also [cancel a Broadcast via the API](/docs/api-reference/broadcasts/cancel-broadcast).

<Note>
  Canceling is only available while a Broadcast is `scheduled` or `queued`.
  Emails that have already been sent cannot be recalled.
</Note>

## Related pages

* [Managing Broadcasts](/docs/dashboard/broadcasts/introduction)
* [Broadcast statuses](/docs/dashboard/broadcasts/manage-broadcasts#understand-broadcast-statuses)
