> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Forward emails with Resend Inbound

> Learn how to forward receiving emails to another email address with Resend Inbound.

Inbound enables you to receive emails with Resend.

This guide demonstrates how to forward received emails using [NextJS](https://nextjs.org/), although you can use any framework you prefer.

<Steps>
  <Step title="Verify a domain with Inbound">
    [Verify a domain](https://resend.com/domains) and enable receiving emails for that domain. We strongly recommend verifying a subdomain (`subdomain.example.com`) instead of the root domain (`example.com`).

    <img alt="Verify a domain with Inbound" src="https://mintcdn.com/resend/Pc2KlUXbYPa-UCHT/images/forward-emails-with-resend-inbound.png?fit=max&auto=format&n=Pc2KlUXbYPa-UCHT&q=85&s=bb522c39f8fc29fafeda1166be728cca" width="3736" height="1916" data-path="images/forward-emails-with-resend-inbound.png" />

    Add the records in your DNS provider and wait for verification to finish in Resend. Learn more about [adding Domains in Resend](/docs/dashboard/domains/introduction).

    <Warning>
      When you enable Inbound on a domain, Resend receives *all emails* sent to that
      specific domain depending on the priority of the MX record. For this reason,
      we strongly recommend verifying a subdomain (`subdomain.example.com`) instead
      of the root domain (`example.com`). Learn more about [avoiding conflicts with
      your existing MX
      records](/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records).
    </Warning>
  </Step>

  <Step title="Create a POST route">
    Resend can send a webhook to your application's endpoint every time you receive an email.

    Add a new POST route to your application's endpoint.

    ```ts app/api/inbound-webhook/route.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    import type { NextRequest } from 'next/server';
    import { NextResponse } from 'next/server';

    export const POST = async (request: NextRequest) => {
      try {
        const payload = await request.text();

        return NextResponse.json(payload);
      } catch (error) {
        console.error(error);
        return new NextResponse(`Error: ${error}`, { status: 500 });
      }
    };
    ```
  </Step>

  <Step title="Create a webhook in Resend">
    Go to the [Webhooks page](https://resend.com/webhooks) and click **Add Webhook**.

    1. Add your publicly accessible HTTPS URL.
    2. Select all events you want to observe (e.g., `email.received`).
    3. Click **Add**.

    <img alt="Create a webhook in Resend" src="https://mintcdn.com/resend/Pc2KlUXbYPa-UCHT/images/forward-emails-with-resend-inbound-1.png?fit=max&auto=format&n=Pc2KlUXbYPa-UCHT&q=85&s=43a04cb717556ed636109764863bf44a" width="3736" height="1916" data-path="images/forward-emails-with-resend-inbound-1.png" />

    <Tip>
      For development, you can create a tunnel to your localhost server using a tool like
      [ngrok](https://ngrok.com/download) or [VS Code Port Forwarding](https://code.visualstudio.com/docs/debugtest/port-forwarding). These tools serve your local dev environment at a public URL you can use to test your local webhook endpoint.

      Example: `https://example123.ngrok.io/api/webhook`
    </Tip>
  </Step>

  <Step title="Add Resend to your project">
    Add the Resend Node.js SDK to your project using your preferred package manager.

    <CodeGroup>
      ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
      npm install resend
      ```

      ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
      yarn add resend
      ```

      ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
      pnpm add resend
      ```

      ```bash bun theme={"theme":{"light":"github-light","dark":"vesper"}}
      bun add resend
      ```
    </CodeGroup>

    Create an [API key with "Full access" permission](/docs/dashboard/api-keys/introduction) in Resend and add it to your project's .env file.

    ```env .env theme={"theme":{"light":"github-light","dark":"vesper"}}
    RESEND_API_KEY=re_xxxxxxxxx
    ```
  </Step>

  <Step title="Verify the webhook request">
    Webhook signing secrets are used to validate the payload data sent to your application from Resend.

    Update your POST route to verify the webhook request using the webhook secret. First, copy the webhook secret from the webhook details page.

    <img alt="Webhook Secret" src="https://mintcdn.com/resend/Pc2KlUXbYPa-UCHT/images/forward-emails-with-resend-inbound-2.png?fit=max&auto=format&n=Pc2KlUXbYPa-UCHT&q=85&s=1f5b8a6ea354470d05869f61ffb087ec" width="3736" height="1916" data-path="images/forward-emails-with-resend-inbound-2.png" />

    Then, add it to your project's .env file.

    ```env .env theme={"theme":{"light":"github-light","dark":"vesper"}}
    RESEND_WEBHOOK_SECRET=whsec_xxxxxxxxxx
    ```

    Update the POST route to verify the webhook request using the webhook secret.

    <Tip>
      Make sure that you’re using the raw request body when verifying webhooks. The cryptographic signature is sensitive to even the slightest change. Some frameworks parse the request as JSON and then stringify it, and this will also break the signature verification.
    </Tip>

    ```ts app/api/inbound-webhook/route.ts {3, 5, 12-32} theme={"theme":{"light":"github-light","dark":"vesper"}}
    import type { NextRequest } from 'next/server';
    import { NextResponse } from 'next/server';
    import { Resend } from 'resend';

    const resend = new Resend(process.env.RESEND_API_KEY);

    export async function POST(req: NextRequest) {
      try {
        // we need raw request text to verify the webhook
        const payload = await req.text();

        const id = req.headers.get('svix-id');
        const timestamp = req.headers.get('svix-timestamp');
        const signature = req.headers.get('svix-signature');

        if (!id || !timestamp || !signature) {
          return new NextResponse('Missing headers', { status: 400 });
        }

        // Throws an error if the webhook is invalid
        // Otherwise, returns the parsed payload object
        const result = resend.webhooks.verify({
          payload,
          headers: {
            id,
            timestamp,
            signature,
          },
          webhookSecret: process.env.RESEND_WEBHOOK_SECRET!,
        });

        return NextResponse.json(result);
      } catch (error) {
        console.error(error);
        return new NextResponse(`Error: ${error}`, { status: 500 });
      }
    }
    ```
  </Step>

  <Step title="Process incoming emails">
    Once you verify the webhook, it returns the webhook payload as a JSON object. You can use this payload to forward the email to another email address. Note the following steps:

    1. Add a guard clause to ensure the event type is `email.received`.
    2. Get the incoming email's content
    3. Download and encode any attachments
    4. Forward the email (remember to update the `from` and `to` addresses below)

    <Info>
      Webhooks do not include the email body, headers, or attachments, only their
      metadata. You must call the [Received emails
      API](/docs/api-reference/emails/retrieve-received-email) or the [Attachments
      API](/docs/api-reference/emails/list-received-email-attachments) to retrieve them.
      This design choice supports large attachments in serverless environments that
      have limited request body sizes.
    </Info>

    ```ts app/api/inbound-webhook/route.ts {29, 34, 42, 67} theme={"theme":{"light":"github-light","dark":"vesper"}}
    import type { NextRequest } from 'next/server';
    import { NextResponse } from 'next/server';
    import { Resend, type ListAttachmentsResponseSuccess } from 'resend';

    const resend = new Resend(process.env.RESEND_API_KEY);

    export async function POST(req: NextRequest) {
      try {
        const payload = await req.text();

        const id = req.headers.get('svix-id');
        const timestamp = req.headers.get('svix-timestamp');
        const signature = req.headers.get('svix-signature');

        if (!id || !timestamp || !signature) {
          return new NextResponse('Missing headers', { status: 400 });
        }

        const result = resend.webhooks.verify({
          payload,
          headers: {
            id,
            timestamp,
            signature,
          },
          webhookSecret: process.env.RESEND_WEBHOOK_SECRET!,
        });

        // 1. Add a guard clause to ensure the event type is `email.received`.
        if (result.type !== 'email.received') {
          return NextResponse.json({ message: 'Invalid event' }, { status: 200 });
        }

        // 2. Get the incoming email's content
        const { data: email, error: emailError } =
          await resend.emails.receiving.get(result.data.email_id);

        if (emailError) {
          throw new Error(`Failed to fetch email: ${emailError.message}`);
        }

        // 3. Download and encode any attachments
        const { data: attachmentsData, error: attachmentsError } =
          await resend.emails.receiving.attachments.list({
            emailId: result.data.email_id,
          });

        if (attachmentsError) {
          throw new Error(
            `Failed to fetch attachments: ${attachmentsError.message}`,
          );
        }

        const attachments =
          attachmentsData?.data as ListAttachmentsResponseSuccess['data'] &
            { content: string }[];

        if (attachments && attachments.length > 0) {
          // download the attachments and encode them in base64
          for (const attachment of attachments) {
            const response = await fetch(attachment.download_url);
            const buffer = Buffer.from(await response.arrayBuffer());
            attachment.content = buffer.toString('base64');
          }
        }

        // 4. Forward the email
        const { data, error: sendError } = await resend.emails.send({
          from: 'onboarding@resend.dev', // replace with an email address from your verified domain
          to: ['delivered@resend.dev'], // replace with the email address you want to forward the email to
          subject: result.data.subject,
          html: email.html,
          text: email.text,
          attachments,
        });

        if (sendError) {
          throw new Error(`Failed to forward email: ${sendError.message}`);
        }

        return NextResponse.json({ message: 'Email forwarded successfully', data });
      } catch (error) {
        console.error(error);
        return new NextResponse(`Error: ${error}`, { status: 500 });
      }
    }
    ```
  </Step>

  <Step title="Test the endpoint">
    You can test the endpoint by sending an email to the domain you verified.

    For example, if you verified `marketing.example.com`, send an email to `test@marketing.example.com`.

    * Try a simple HTML email with a subject and a body.
    * Try an email with an attachment or multiple attachments.

    You can view the received email in the [Emails page](https://resend.com/emails/receiving) and see the webhook payload in the [Webhooks page](https://resend.com/webhooks).
  </Step>

  <Step title="Go to Production">
    Once you've tested the endpoint:

    1. Publish your application to your production environment.
    2. Add your production POST endpoint as a new webhook in Resend.
  </Step>
</Steps>
