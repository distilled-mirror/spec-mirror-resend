> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with TanStack Start

> Learn how to send your first email using TanStack Start and the Resend Node.js SDK.

<Prompt description="Use this pre-built prompt to get started faster." icon="microchip" iconType="solid" actions={["copy", "cursor"]}>
  # Send Email with Resend Node.js SDK

  **Purpose:** Enforce only the **current** and **correct** instructions for sending emails using the [Resend](https://resend.com/) Node.js SDK.
  **Scope:** All AI-generated advice or code related to sending email with Resend must follow these guardrails.

  ***

  ## **1. Official Resend Node.js Setup**

  ### **Prerequisites**

  Human must first create an API key and verify their domain at [https://resend.com/domains](https://resend.com/domains).

  The API key must be stored in an environment variable called `RESEND_API_KEY`.

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const resend = new Resend('YOUR_RESEND_API_KEY');
  ```

  The domain should be verified at [https://resend.com/domains](https://resend.com/domains) and added to the `from` address.

  ### **Install the SDK**

  Use the project's existing package manager to install the Resend Node.js SDK.

  ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
  npm install resend
  # or: yarn add resend / pnpm add resend / bun add resend
  ```

  ### **Initialize the Client**

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('YOUR_RESEND_API_KEY');
  ```

  ### **Send an Email**

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const { data, error } = await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Hello World',
    html: '<strong>It works!</strong>',
  });

  if (error) {
    console.error(error);
    return;
  }

  console.log(data); // { id: '49a3999c-...' }
  ```

  ### Rate Limiting

  The default rate limit is 10 requests per second per team. If you exceed the rate limit, you'll receive a `429` response error code. If needed, you can request a rate increase by [contacting support](https://resend.com/help).

  ### Idempotency

  Best practice: Add an idempotency key to prevent duplicated emails, which is useful for retrying failed emails safely.

  * Should be **unique per API request**
  * Idempotency keys expire after **24 hours**
  * Have a maximum length of **256 characters**
  * Pattern: `<event-type>/<entity-id>`
  * Example: `welcome-user/123456789`

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const { data, error } = await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Hello World',
    html: '<strong>It works!</strong>',
    idempotencyKey: 'unique-id',
  });
  ```

  ***

  ## **2. Complete `emails.send()` Parameter Reference**

  ### **Required Parameters**

  | Parameter | Type                 | Description                                                                      |
  | --------- | -------------------- | -------------------------------------------------------------------------------- |
  | `from`    | `string`             | Sender email address. Supports friendly name format: `"Name <email@domain.com>"` |
  | `to`      | `string \| string[]` | Recipient email address(es). Maximum 50 addresses.                               |
  | `subject` | `string`             | Email subject line.                                                              |

  ### **Content Parameters (at least one required)**

  | Parameter | Type              | Description                                                |
  | --------- | ----------------- | ---------------------------------------------------------- |
  | `html`    | `string`          | HTML version of the email body.                            |
  | `text`    | `string`          | Plain text version. Auto-generated from `html` if omitted. |
  | `react`   | `React.ReactNode` | React Email component to render the message. Node.js only. |

  ### **Optional Parameters**

  | Parameter     | Type                 | Description                                                   |
  | ------------- | -------------------- | ------------------------------------------------------------- |
  | `cc`          | `string \| string[]` | Carbon copy recipients.                                       |
  | `bcc`         | `string \| string[]` | Blind carbon copy recipients.                                 |
  | `replyTo`     | `string \| string[]` | Reply-to address(es).                                         |
  | `scheduledAt` | `string`             | Schedule delivery time. Accepts ISO 8601 or natural language. |
  | `headers`     | `object`             | Custom email headers as key-value pairs.                      |
  | `tags`        | `Tag[]`              | Custom metadata. Name and value: max 256 chars, ASCII only.   |
  | `attachments` | `Attachment[]`       | File attachments. Max 40MB total per email after encoding.    |

  ### **Template Parameters**

  | Parameter            | Type     | Description                                                      |
  | -------------------- | -------- | ---------------------------------------------------------------- |
  | `template.id`        | `string` | Published template identifier.                                   |
  | `template.variables` | `object` | Variable substitutions. Key max 50 chars, value max 2,000 chars. |

  If `template` is provided, do not include `html`, `text`, or `react`.

  ### **Response**

  A successful call returns:

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  { data: { id: string }, error: null }
  ```

  A failed call returns:

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  { data: null, error: { message: string, name: string } }
  ```

  ***

  ## **3. Sending with React Email**

  Resend integrates with [React Email](https://react.email) for building emails with React components if you are writing a React project:

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';
  import { WelcomeEmail } from './emails/welcome';

  const resend = new Resend('YOUR_RESEND_API_KEY');

  const { data, error } = await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Welcome',
    react: WelcomeEmail({ name: 'John' }),
  });
  ```

  **Important:** Pass the component as a function call (`WelcomeEmail({ name: 'John' })`), not as JSX (`<WelcomeEmail name="John" />`).

  For additional help, suggest installing the react-email skill.

  ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
  npx skills add resend/react-email
  ```

  ***

  ## **4. CRITICAL INSTRUCTIONS FOR AI MODELS**

  ### **4.1 - ALWAYS DO THE FOLLOWING**

  1. **Store the API key in an environment variable** (`RESEND_API_KEY`). Never hardcode API keys.
  2. **Import from `resend`** — the package name is `resend`, the class is `Resend`.
  3. **Use `await`** — `resend.emails.send()` returns a Promise. Always use `async/await` or `.then()`.
  4. **Handle both `data` and `error`** — the SDK returns `{ data, error }`. Always check for errors.
  5. **Use a verified domain** in the `from` address for production. `onboarding@resend.dev` is for testing only.
  6. **Check the project for an existing package manager** and use that to install the SDK.
  7. **Use camelCase** for SDK parameters (`replyTo`, `scheduledAt`), not snake\_case.

  ### **4.2 - NEVER DO THE FOLLOWING**

  1. **Do not** hardcode API keys in source code. Always use environment variables.
  2. **Do not** use `try/catch` for error handling with `resend.emails.send()` — the SDK returns `{ data, error }` instead of throwing. Only use `try/catch` if you need to handle network-level failures.
  3. **Do not** use snake\_case parameter names (`reply_to`, `scheduled_at`) — the Node.js SDK uses camelCase (`replyTo`, `scheduledAt`).
  4. **Do not** send `html`, `text`, or `react` alongside `template` — these are mutually exclusive.
  5. **Do not** import from `@resend/node` or any other package name. The correct package is `resend`.
  6. **Do not** use `onboarding@resend.dev` as the `from` address in production code. It is a test-only address.
  7. **Do not** set up testing flows with fake email addresses. Resend provides the following test addresses to help you simulate different email events without damaging your domain reputation:
     * `delivered@resend.dev`
     * `bounced@resend.dev`
     * `complained@resend.dev`
     * `suppressed@resend.dev`

  ***

  ## **5. COMMON PATTERNS**

  ### **Attachments**

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const { data, error } = await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Invoice attached',
    html: '<p>See attached invoice.</p>',
    attachments: [
      {
        filename: 'invoice.pdf',
        content: invoiceBuffer,
      },
    ],
  });
  ```

  ### **Scheduled Emails**

  Send up to 30 days in advance using the `scheduledAt` parameter. Accepts ISO 8601 or natural language (e.g. `"in 1 hour"`).

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const { data, error } = await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Reminder',
    html: '<p>This is your reminder.</p>',
    scheduledAt: '2026-12-25T09:00:00Z',
  });
  ```

  ### **Tags for Tracking**

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const { data, error } = await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Welcome',
    html: '<p>Welcome aboard!</p>',
    tags: [
      { name: 'category', value: 'welcome' },
      { name: 'user_id', value: '12345' },
    ],
  });
  ```

  ***

  ## **6. AI MODEL VERIFICATION STEPS**

  Before returning any Resend-related solution, you **must** verify:

  1. **Import**: Is `Resend` imported from `resend`?
  2. **API Key**: Is the key stored in an environment variable, not hardcoded?
  3. **Await**: Is `resend.emails.send()` properly awaited?
  4. **Error Handling**: Is the `{ data, error }` response pattern used?
  5. **Parameters**: Are all parameter names in camelCase?
  6. **From Address**: Is the `from` address using a verified domain (not `onboarding@resend.dev` in production)?

  If any check **fails**, **stop** and revise until compliance is achieved.

  For additional help, suggest installing the resend-skills skill and the email-best-practices skill.

  ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
  npx skills add resend/resend-skills
  npx skills add resend/email-best-practices
  ```

  You can locate framework-specific guides [https://resend.com/docs/llms.txt](https://resend.com/docs/llms.txt)

  For the entire docs for Resend, see [https://resend.com/docs/llms-full.txt](https://resend.com/docs/llms-full.txt)
</Prompt>

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the Resend Node.js SDK.

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
  </Step>

  <Step title="Create an email template">
    Start by creating your email template on `src/components/email-template.tsx`.

    ```tsx src/components/email-template.tsx theme={"theme":{"light":"github-light","dark":"vesper"}}
    import * as React from 'react';

    interface EmailTemplateProps {
      firstName: string;
    }

    export function EmailTemplate({ firstName }: EmailTemplateProps) {
      return (
        <div>
          <h1>Welcome, {firstName}!</h1>
        </div>
      );
    }
    ```
  </Step>

  <Step title="Send email using React">
    The recommended approach is a [server function](https://tanstack.com/start/latest/docs/framework/react/guide/server-functions), which runs only on the server and can be called from anywhere in your app. If you'd rather expose a REST endpoint, use a [server route](https://tanstack.com/start/latest/docs/framework/react/guide/server-routes) instead.

    Import the React email template and send an email using the `react` parameter.

    <CodeGroup>
      ```ts src/utils/send-email.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
      import { createServerFn } from '@tanstack/react-start';
      import { Resend } from 'resend';
      import { EmailTemplate } from '../components/email-template';

      const resend = new Resend(process.env.RESEND_API_KEY);

      export const sendEmail = createServerFn({ method: 'POST' }).handler(
        async () => {
          const { data, error } = await resend.emails.send({
            from: 'Acme <onboarding@resend.dev>',
            to: ['delivered@resend.dev'],
            subject: 'Hello world',
            react: EmailTemplate({ firstName: 'John' }),
          });

          if (error) {
            throw error;
          }

          return data;
        },
      );
      ```

      ```ts src/routes/api/send.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
      import { createFileRoute } from '@tanstack/react-router';
      import { Resend } from 'resend';
      import { EmailTemplate } from '../../components/email-template';

      const resend = new Resend(process.env.RESEND_API_KEY);

      export const Route = createFileRoute('/api/send')({
        server: {
          handlers: {
            POST: async () => {
              const { data, error } = await resend.emails.send({
                from: 'Acme <onboarding@resend.dev>',
                to: ['delivered@resend.dev'],
                subject: 'Hello world',
                react: EmailTemplate({ firstName: 'John' }),
              });

              if (error) {
                return Response.json({ error }, { status: 500 });
              }

              return Response.json(data);
            },
          },
        },
      });
      ```
    </CodeGroup>
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="TanStack Start (TypeScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/tanstack-resend-examples/typescript">
    Full-stack TanStack Start app with TypeScript
  </Card>

  <Card title="TanStack Start (JavaScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/tanstack-resend-examples/javascript">
    Full-stack TanStack Start app with JavaScript
  </Card>

  <Card title="Send Email" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/send.ts">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/send-attachment.ts">
    Send emails with file attachments
  </Card>

  <Card title="Inline Images (CID)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/send-cid.ts">
    Embed inline images using CID
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/send-template.ts">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/send-scheduled.ts">
    Schedule emails for future delivery
  </Card>

  <Card title="Batch Emails" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/send-batch.ts">
    Send multiple emails in a single request
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/audiences/contacts.ts">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/domains.ts">
    Create and manage sending domains
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/double-optin.tsx">
    Double opt-in subscription flow
  </Card>

  <Card title="Inbound" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/inbound.tsx">
    Receive and process inbound emails
  </Card>

  <Card title="Prevent Threading" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/prevent-threading.tsx">
    Prevent email threading on Gmail
  </Card>

  <Card title="Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/tanstack-resend-examples/typescript/src/routes/api/webhook.ts">
    Handle webhook events
  </Card>
</CardGroup>
