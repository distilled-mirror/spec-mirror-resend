> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Event Types

> List of supported event types and their payload.

## Email Events

<div>
  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.bounced`](/docs/webhooks/emails/bounced)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the recipient's mail server **permanently rejected the
      email**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#BAA7FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.clicked`](/docs/webhooks/emails/clicked)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **recipient clicks on an email link**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FFCA16',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.complained`](/docs/webhooks/emails/complained)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the email was successfully **delivered, but the recipient
      marked it as spam**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.delivered`](/docs/webhooks/emails/delivered)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever Resend **successfully delivered the email** to the
      recipient's mail server.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#B5B3AD',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.delivery_delayed`](/docs/webhooks/emails/delivery-delayed)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **email couldn't be delivered due to a temporary
      issue**. Delivery delays can occur, for example, when the recipient's
      inbox is full, or when the receiving email server experiences a transient
      issue.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.failed`](/docs/webhooks/emails/failed)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **email failed to send due to an error**. This event
      is triggered when there are issues such as invalid recipients, API key
      problems, domain verification issues, email quota limits, or other sending
      failures.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.opened`](/docs/webhooks/emails/opened)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **recipient opened the email**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#4CCCE6',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.received`](/docs/webhooks/emails/received)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever Resend **successfully receives an email**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#B5B2BC',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.scheduled`](/docs/webhooks/emails/scheduled)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **email is scheduled to be sent**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#B5B3AD',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.sent`](/docs/webhooks/emails/sent)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **API request was successful**. Resend will attempt to
      deliver the message to the recipient's mail server.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#D4B3A5',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`email.suppressed`](/docs/webhooks/emails/suppressed)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **email is suppressed** by Resend.
    </div>
  </div>
</div>

## Domain Events

<div>
  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`domain.created`](/docs/webhooks/domains/created)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs when a **domain was successfully created**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`domain.updated`](/docs/webhooks/domains/updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs when a **domain was successfully updated**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`domain.deleted`](/docs/webhooks/domains/deleted)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs when a **domain was successfully deleted**.
    </div>
  </div>
</div>

## Contact Events

<div>
  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`contact.created`](/docs/webhooks/contacts/created)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **contact was successfully created**.
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      *Note: When importing multiple contacts using CSV, these events won't be
      triggered. [Contact support](https://resend.com/help) if you have any
      questions.*
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`contact.updated`](/docs/webhooks/contacts/updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **contact was successfully updated**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`contact.deleted`](/docs/webhooks/contacts/deleted)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **contact was successfully deleted**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`contact.topics.updated`](/docs/webhooks/contacts/topics-updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **contact's topic subscriptions change**.
    </div>
  </div>
</div>

## Suppression Events

<div>
  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`suppression.added`](/docs/webhooks/suppressions/added)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **email address is added to your suppression list**,
      automatically after a hard bounce or spam complaint, or manually through
      the dashboard or API.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`suppression.removed`](/docs/webhooks/suppressions/removed)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **email address is removed from your suppression
      list**.
    </div>
  </div>
</div>

## Topic Events

<div>
  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`topic.created`](/docs/webhooks/topics/created)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **topic is created**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`topic.updated`](/docs/webhooks/topics/updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **topic is updated**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`topic.deleted`](/docs/webhooks/topics/deleted)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **topic is deleted**.
    </div>
  </div>
</div>

## Inbox Events

Inboxes are in private beta. Every inbox event's `data` has `source` and `inbox_id`, plus the IDs and objects that apply to the event. Keys that don't apply are left out, not sent as `null`.

The `thread`, `email`, `draft` and `inbox` objects are loaded when the webhook is sent, not when the change happened, so two quick changes can both show the second state. `email` and `draft` leave out `html` and `text`; fetch the body from the API. Retries keep the same `svix-id` header, so dedupe on it.

<div>
  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.created`](/docs/webhooks/inboxes/created)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **inbox is created**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.updated`](/docs/webhooks/inboxes/updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **inbox's settings change**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.deleted`](/docs/webhooks/inboxes/deleted)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **inbox is deleted**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.thread.created`](/docs/webhooks/inboxes/thread-created)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever the **first email of a thread** lands in the inbox,
      inbound or outbound.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.thread.folder.updated`](/docs/webhooks/inboxes/thread-folder-updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **thread moves between folders**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#BAA7FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.thread.assigned`](/docs/webhooks/inboxes/thread-assigned)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **thread is assigned or reassigned**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#B5B2BC',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.thread.unassigned`](/docs/webhooks/inboxes/thread-unassigned)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **thread is unassigned**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.thread.labels.updated`](/docs/webhooks/inboxes/thread-labels-updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **label is applied to or removed from a thread**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#4CCCE6',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.email.received`](/docs/webhooks/inboxes/email-received)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **inbound email is added to a thread**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#B5B3AD',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.email.sent`](/docs/webhooks/inboxes/email-sent)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever an **outbound email is accepted for delivery** and added
      to a thread.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#3DD68C',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.draft.created`](/docs/webhooks/inboxes/draft-created)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **draft is created**, standalone or reply.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#70B8FF',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.draft.updated`](/docs/webhooks/inboxes/draft-updated)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **draft is edited**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#B5B3AD',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.draft.sent`](/docs/webhooks/inboxes/draft-sent)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **draft is sent**.
    </div>
  </div>

  <div style={{ marginBottom: '32px' }}>
    <div>
      <span
        style={{
      display: 'inline-block',
      width: '8px',
      height: '8px',
      borderRadius: '50%',
      backgroundColor: '#FF9592',
      verticalAlign: 'middle',
      marginRight: '6px',
    }}
      />

      {' '}

      [`inbox.draft.deleted`](/docs/webhooks/inboxes/draft-deleted)
    </div>

    <div style={{ marginLeft: '20px', marginTop: '4px' }}>
      Occurs whenever a **draft is discarded**.
    </div>
  </div>
</div>
