> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Appwrite and Resend

> Learn how to send emails through Resend using Appwrite Messaging.

[Appwrite](https://appwrite.io) is an open-source development platform for building and scaling applications faster, offering Auth, Databases, Storage, Functions, Messaging, Realtime, and web hosting, all in one place.

Appwrite Messaging includes a native Resend provider, so you can send emails to your app's users through Resend without writing any delivery code.

## Prerequisites

To get the most out of this guide, you'll need to:

* [Create an API key](https://resend.com/api-keys)
* [Verify your domain](https://resend.com/domains)

You'll also need an [Appwrite project](https://cloud.appwrite.io) with at least one user.

## 1. Add Resend as an email provider

In the Appwrite Console, navigate to **Messaging** > **Providers** > **Add provider** > **Email**. Give your provider a name, choose **Resend**, and click **Save and continue**.

<Note>
  The provider will be saved to your project, but not enabled until you complete
  its configuration.
</Note>

In the **Configure** step, you will need to provide details from your Resend dashboard to connect your Appwrite project:

| Field          | Description                                                                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API key        | Head to API Keys > Create API Key. You can also follow [Resend's instructions](/docs/dashboard/api-keys/introduction) to create an API key.                        |
| Sender email   | The provider sends emails from this sender email. The sender email needs to be an email under a [verified domain](/docs/dashboard/domains/introduction) in Resend. |
| Sender name    | The sender name that appears in the emails sent from this provider.                                                                                           |
| Reply-to email | The reply-to email that appears in the emails sent from this provider.                                                                                        |
| Reply-to name  | The reply-to name that appears in the emails sent from this provider.                                                                                         |

After adding these details, click **Save and continue** to enable the provider.

## 2. Add recipients

Appwrite Messaging delivers messages to **targets**, the different ways a user can be reached: their email addresses, phone numbers, and devices with your app installed. Targets can subscribe to **topics**, so when a message is published to a topic, all subscribed targets receive it.

Users with verified emails who signed up with [email password](https://appwrite.io/docs/products/auth/email-password), [magic URL](https://appwrite.io/docs/products/auth/magic-url), [email OTP](https://appwrite.io/docs/products/auth/email-otp), or [OAuth2](https://appwrite.io/docs/products/auth/oauth2) login already have an email target. You can also add targets to existing users by navigating to **Authentication** > **Users** > select a user > **Targets**.

To message groups of users, navigate to **Messaging** > **Topics** > **Create topic** and subscribe their targets to the topic.

Learn more about [topics](https://appwrite.io/docs/products/messaging/topics) and [targets](https://appwrite.io/docs/products/messaging/targets) in the Appwrite documentation.

## 3. Send your first email

To send a test email from the Appwrite Console, navigate to **Messaging** > **Messages** > **Create message** > **Email**. Add your message and in the targets step, select one of your test targets. Set the schedule to **Now** and click **Send**.

Verify that you can receive the message in your inbox. If not, check for logs in the Appwrite Console or in your [Resend dashboard](https://resend.com/emails).

To send emails programmatically, use an [Appwrite Server SDK](https://appwrite.io/docs/sdks#server):

```js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Client, Messaging, ID } from 'node-appwrite';

const client = new Client()
  .setEndpoint('https://<REGION>.cloud.appwrite.io/v1') // Your API endpoint
  .setProject('<PROJECT_ID>') // Your project ID
  .setKey('<API_KEY>'); // Your secret API key

const messaging = new Messaging(client);

const message = await messaging.createEmail({
  messageId: ID.unique(),
  subject: 'Welcome aboard!',
  content: 'Thanks for signing up. We are happy to have you.',
  topics: ['<TOPIC_ID>'],
});
```

Emails can be sent immediately or scheduled for a later time.
