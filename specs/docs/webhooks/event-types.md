> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Event Types

> List of supported event types and their payload.

## Email Events

&#x20;

[`email.bounced`](/docs/webhooks/emails/bounced)

Occurs whenever the recipient's mail server **permanently rejected the
email**.

&#x20;

[`email.clicked`](/docs/webhooks/emails/clicked)

Occurs whenever the **recipient clicks on an email link**.

&#x20;

[`email.complained`](/docs/webhooks/emails/complained)

Occurs whenever the email was successfully **delivered, but the recipient
marked it as spam**.

&#x20;

[`email.delivered`](/docs/webhooks/emails/delivered)

Occurs whenever Resend **successfully delivered the email** to the
recipient's mail server.

&#x20;

[`email.delivery_delayed`](/docs/webhooks/emails/delivery-delayed)

Occurs whenever the **email couldn't be delivered due to a temporary
issue**. Delivery delays can occur, for example, when the recipient's
inbox is full, or when the receiving email server experiences a transient
issue.

&#x20;

[`email.failed`](/docs/webhooks/emails/failed)

Occurs whenever the **email failed to send due to an error**. This event
is triggered when there are issues such as invalid recipients, API key
problems, domain verification issues, email quota limits, or other sending
failures.

&#x20;

[`email.opened`](/docs/webhooks/emails/opened)

Occurs whenever the **recipient opened the email**.

&#x20;

[`email.received`](/docs/webhooks/emails/received)

Occurs whenever Resend **successfully receives an email**.

&#x20;

[`email.scheduled`](/docs/webhooks/emails/scheduled)

Occurs whenever the **email is scheduled to be sent**.

&#x20;

[`email.sent`](/docs/webhooks/emails/sent)

Occurs whenever the **API request was successful**. Resend will attempt to
deliver the message to the recipient's mail server.

&#x20;

[`email.suppressed`](/docs/webhooks/emails/suppressed)

Occurs whenever the **email is suppressed** by Resend.

## Domain Events

&#x20;

[`domain.created`](/docs/webhooks/domains/created)

Occurs when a **domain was successfully created**.

&#x20;

[`domain.updated`](/docs/webhooks/domains/updated)

Occurs when a **domain was successfully updated**.

&#x20;

[`domain.deleted`](/docs/webhooks/domains/deleted)

Occurs when a **domain was successfully deleted**.

## Contact Events

&#x20;

[`contact.created`](/docs/webhooks/contacts/created)

Occurs whenever a **contact was successfully created**.

*Note: When importing multiple contacts using CSV, these events won't be
triggered. [Contact support](https://resend.com/help) if you have any
questions.*

&#x20;

[`contact.updated`](/docs/webhooks/contacts/updated)

Occurs whenever a **contact was successfully updated**.

&#x20;

[`contact.deleted`](/docs/webhooks/contacts/deleted)

Occurs whenever a **contact was successfully deleted**.

&#x20;

[`contact.topics.updated`](/docs/webhooks/contacts/topics-updated)

Occurs whenever a **contact's topic subscriptions change**.

## Suppression Events

&#x20;

[`suppression.added`](/docs/webhooks/suppressions/added)

Occurs whenever an **email address is added to your suppression list**,
automatically after a hard bounce or spam complaint, or manually through
the dashboard or API.

&#x20;

[`suppression.removed`](/docs/webhooks/suppressions/removed)

Occurs whenever an **email address is removed from your suppression
list**.

## Topic Events

&#x20;

[`topic.created`](/docs/webhooks/topics/created)

Occurs whenever a **topic is created**.

&#x20;

[`topic.updated`](/docs/webhooks/topics/updated)

Occurs whenever a **topic is updated**.

&#x20;

[`topic.deleted`](/docs/webhooks/topics/deleted)

Occurs whenever a **topic is deleted**.

## Inbox Events

Every inbox event's `data` has `source` and `inbox_id`, plus the IDs and objects that apply to the event. Keys that don't apply are left out, not sent as `null`.

The `thread`, `email`, `draft` and `inbox` objects are loaded when the webhook is sent, not when the change happened, so two quick changes can both show the second state. `email` and `draft` leave out `html` and `text`; fetch the body from the API. Retries keep the same `svix-id` header, so dedupe on it.

&#x20;

[`inbox.created`](/docs/webhooks/inboxes/created)

Occurs whenever an **inbox is created**.

&#x20;

[`inbox.updated`](/docs/webhooks/inboxes/updated)

Occurs whenever an **inbox's settings change**.

&#x20;

[`inbox.deleted`](/docs/webhooks/inboxes/deleted)

Occurs whenever an **inbox is deleted**.

&#x20;

[`inbox.thread.created`](/docs/webhooks/inboxes/thread-created)

Occurs whenever the **first email of a thread** lands in the inbox,
inbound or outbound.

&#x20;

[`inbox.thread.folder.updated`](/docs/webhooks/inboxes/thread-folder-updated)

Occurs whenever a **thread moves between folders**.

&#x20;

[`inbox.thread.assigned`](/docs/webhooks/inboxes/thread-assigned)

Occurs whenever a **thread is assigned or reassigned**.

&#x20;

[`inbox.thread.unassigned`](/docs/webhooks/inboxes/thread-unassigned)

Occurs whenever a **thread is unassigned**.

&#x20;

[`inbox.thread.labels.updated`](/docs/webhooks/inboxes/thread-labels-updated)

Occurs whenever a **label is applied to or removed from a thread**.

&#x20;

[`inbox.email.received`](/docs/webhooks/inboxes/email-received)

Occurs whenever an **inbound email is added to a thread**.

&#x20;

[`inbox.email.sent`](/docs/webhooks/inboxes/email-sent)

Occurs whenever an **outbound email is accepted for delivery** and added
to a thread.

&#x20;

[`inbox.draft.created`](/docs/webhooks/inboxes/draft-created)

Occurs whenever a **draft is created**, standalone or reply.

&#x20;

[`inbox.draft.updated`](/docs/webhooks/inboxes/draft-updated)

Occurs whenever a **draft is edited**.

&#x20;

[`inbox.draft.sent`](/docs/webhooks/inboxes/draft-sent)

Occurs whenever a **draft is sent**.

&#x20;

[`inbox.draft.deleted`](/docs/webhooks/inboxes/draft-deleted)

Occurs whenever a **draft is discarded**.
