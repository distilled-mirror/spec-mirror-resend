> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Supabase Edge Functions

> Learn how to send your first email using Supabase Edge Functions.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

Make sure you have the latest version of the [Supabase CLI](https://supabase.com/docs/guides/cli#installation) installed.

## Guide

**1. Create Supabase function**

Create a new function locally:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
supabase functions new resend
```

**2. Edit the handler function**

Paste the following code into the `index.ts` file:

```ts index.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
const RESEND_API_KEY = Deno.env.get('RESEND_API_KEY');

const handler = async (_request: Request): Promise<Response> => {
  const res = await fetch('https://api.resend.com/emails', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${RESEND_API_KEY}`,
    },
    body: JSON.stringify({
      from: 'Acme <onboarding@resend.dev>',
      to: ['delivered@resend.dev'],
      subject: 'hello world',
      html: '<strong>it works!</strong>',
    }),
  });

  const data = await res.json();

  return new Response(JSON.stringify(data), {
    status: 200,
    headers: {
      'Content-Type': 'application/json',
    },
  });
};

Deno.serve(handler);
```

**3. Deploy and send email**

Run function locally:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
supabase functions start
supabase functions serve resend --no-verify-jwt
```

Deploy function to Supabase:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
supabase functions deploy resend
```

Open the endpoint URL to send an email:

![Supabase Edge Functions - Deploy Function](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/supabase-edge-functions-deploy-function.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=e28cab375d10a57f712e77ff3c888005)

## Examples

> **[Supabase Edge Functions Example](https://github.com/resend/resend-supabase-edge-functions-example)**
>
> See the full source code.
