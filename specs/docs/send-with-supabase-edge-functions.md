> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Supabase Edge Functions

> Learn how to send your first email using Supabase Edge Functions.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

Make sure you have the latest version of the [Supabase CLI](https://supabase.com/docs/guides/cli#installation) installed.

## Guide

<Steps>
  <Step title="Create Supabase function">
    Create a new function locally:

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    supabase functions new resend
    ```
  </Step>

  <Step title="Edit the handler function">
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
  </Step>

  <Step title="Deploy and send email">
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

    <img alt="Supabase Edge Functions - Deploy Function" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/supabase-edge-functions-deploy-function.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=e28cab375d10a57f712e77ff3c888005" width="3414" height="1886" data-path="images/supabase-edge-functions-deploy-function.png" />
  </Step>
</Steps>

## Examples

<Card title="Supabase Edge Functions Example" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-supabase-edge-functions-example">
  See the full source code.
</Card>
