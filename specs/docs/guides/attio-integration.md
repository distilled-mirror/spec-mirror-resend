> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Attio and Resend

> Connect Resend to Attio to create contacts, add people to segments, and send emails from workflows.

[Attio](https://attio.com) is a customer relationship management platform. The Attio [Resend app](https://attio.com/apps/resend) connects Attio workflows and person records to Resend. You can create contacts, add people to segments, and send plain text or template emails without leaving Attio.

For example, when a deal is marked Closed Won, a workflow can create a contact for the buyer, add that person to a segment, and send a welcome email.

The app is available on every Attio plan. A workspace admin connects one API key for the whole workspace. There isn't a separate connection per member. After the app is connected, every member can run the workflow steps and the record action.

## Connect Resend

<Steps>
  <Step title="Create an API key">
    [Create an API key](https://resend.com/api-keys) in Resend.

    * Use **Full access** when workflows create contacts or add people to segments.
    * Use **Sending access** when you only send email. That permission can't create contacts or update segments.

    You can change the permission later in the [API keys Dashboard](/docs/dashboard/api-keys/introduction).
  </Step>

  <Step title="Install the app in Attio">
    1. In Attio, click your workspace name, then click **Apps and integrations**.
    2. Search for **Resend**, open the app, and click **Install**.
    3. Under **Workspace connection**, click **Connect**.
    4. Paste the API key and click **Add connection**.

    Attio doesn't check the key when you connect it. An invalid key or a missing permission appears when a step or the record action runs.

    Attio documents this setup in the [Resend app article](https://attio.com/help/reference/apps/communication-apps/resend-app).
  </Step>
</Steps>

## Use Resend in a workflow

Add these steps to an [Attio workflow](https://attio.com/help/reference/automations/workflows/create-a-workflow).

### Create contact

Creates a Resend contact from an email address.

* **Email:** The contact's email address. Required.
* **Full name:** The contact's name. Optional.
* **Unsubscribed:** Turn this on to unsubscribe the contact from all Broadcasts. You can't pass a variable for this field.

On success, the step returns the contact ID. Pass that ID into a later step, such as Add contact to segment.

Email identifies the contact in Resend. Run the step again with the same email and Resend updates that contact's name and subscription status. It doesn't create a second contact.

### Add contact to segment

Adds an existing Resend contact to a [segment](/docs/dashboard/contacts/manage-segments).

* **Segment:** The segment to add the contact to. Search the list and pick one. You can't pass a variable for this field. Required.
* **Contact:** The contact to add. Search for a contact, or pass a contact ID from an earlier step. Required.

On success, the step returns the segment ID.

Chain this step after Create contact. Pass that step's contact ID into the contact field.

### Send email

Sends an email through Resend as plain text or from a published [template](/docs/dashboard/templates/introduction).

* **From:** The sending address. Use an address on a [verified domain](/docs/add-a-domain). Required.
* **To:** The recipient's email address. Required.
* **Subject:** The email subject. Required.
* **Plain text:** The email body as plain text.
* **Template:** A published template to send instead of plain text.
* **Template variables:** When you pick a template in the step, Attio adds a text field for each variable that template declares.
* **From name:** The name shown next to the From address. Optional.
* **CC:** Extra recipients to copy. Optional.
* **BCC:** Extra recipients to blind copy. Optional.
* **Reply to:** The address that receives replies. Optional.
* **Schedule:** When to send the email. Leave this empty to send right away. Optional.
* **Tags:** Name and value pairs that label the email in Resend. Optional.
* **Topic:** The [topic](/docs/dashboard/contacts/manage-topics) for this email. Pick it from the list. You can't pass a variable for this field. Optional.
* **Attachments:** Files to attach. Each file needs a filename and a remote file URL. Optional.

Fill in plain text or a template. If you select a template, Attio ignores the plain text body.

On success, the step returns the email ID. Run the same step again and Attio doesn't send a second copy.

<Note>
  The From address has to use a domain you verified in Resend. With the test
  sender `onboarding@resend.dev`, you can only email your own address. [Add a
  domain](/docs/add-a-domain) to email anyone else.
</Note>

<Note>
  If you edit a template in Resend after you configure the step, and the
  template needs a variable you haven't set, the step fails and names the
  missing variable. Open the step and fill in that variable.
</Note>

## Add a person to a segment

You can add one person to a Resend segment from their record, without a workflow.

1. On a person record, open the record menu and click **Add to segment**.
2. If the person has more than one email address, choose which address to use. With one address, Attio shows the field and you can't change it.
3. Select a segment.
4. Click **Add to segment**.

Attio looks up the contact in Resend by email. If no contact exists for that address, Attio creates one and adds it to the segment. If the contact already exists, Attio adds that contact to the segment.

If the action fails, Attio shows the error from Resend and keeps the dialog open so you can correct the issue and try again.

## Fix a failed step

### The key doesn't have permission

An invalid or revoked key fails as unauthorized. A valid key that lacks permission for the action fails with a permission error.

Reconnecting the same key keeps the same permissions. Open the key in the [API keys Dashboard](/docs/dashboard/api-keys/introduction) and grant the permission the action needs, or create a new key and connect that one.

Create contact and Add contact to segment need **Full access**. Send email works with **Sending access**.

### Some fields can't take a variable

The segment on Add contact to segment, and the topic on Send email, come from a list in the step. You pick them when you configure the step. The contact on Add contact to segment can use a variable. The unsubscribed field on Create contact can't use a variable either.
