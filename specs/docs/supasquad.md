> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# SupaSquad + Resend

> A quick jumpstart to using Resend with Supabase for SupaSquad members.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

This guide helps you get started with Resend by:

* [Setting up Resend](#set-up-resend)
* [Send Auth Emails with Resend](#send-auth-emails-with-resend)
* [Send Emails with Supabase Edge Functions](#send-emails-with-supabase-edge-functions)

## Set up Resend

To send emails with your Supabase project, you'll need to first verify it in Resend.

<Steps>
  <Step title="Add a new domain to Resend.">
    Go to the [Domains Dashboard page](https://resend.com/domains) and click on **Add Domain**.
  </Step>

  <Step title="Add your domain name">
    We recommend [using a subdomain](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain) like `updates.example.com`.
  </Step>

  <Step title="Add the DNS records to your DNS provider.">
    Learn more about [setting the required records](/docs/dashboard/domains/introduction) or see the [DNS provider guides](/docs/knowledge-base/) for specific provider instructions.
  </Step>

  <Step title="Confirm in your Dashboard.">
    Click on **I've added the records** to begin the verification process.

    <img alt="Resend Domains page" src="https://mintcdn.com/resend/_kGPo-rF0-rO9nI4/images/resend-domain-records.png?fit=max&auto=format&n=_kGPo-rF0-rO9nI4&q=85&s=24107151c9a59db661aca80c64338bfe" width="3024" height="1900" data-path="images/resend-domain-records.png" />
  </Step>

  <Step title="Wait for the verification to complete.">
    This usually takes 5–10 minutes.
  </Step>
</Steps>

<Info>
  Resend requires you own your domain (i.e., not a shared or public domain).
  Adding DNS records gives Resend the authority to send emails on your behalf
  and signals to the inbox providers that you're a legitimate sender.
</Info>

As a member of the SupaSquad, **you qualify for a discount** on a paid Resend plan. Contact your Supabase representative to get your discount code.

## Send Auth Emails with Resend

If you want to use Resend to send your Supabase Auth Emails, you have three options:

1. [Using the Resend Integration](#using-the-resend-integration): simplest, but less customizable email templates.
2. [Custom Auth Functions](#custom-auth-functions): more customizable email templates, but requires more setup.
3. [Self-hosted with Custom SMTP](#self-hosted-with-custom-smtp): only for those self-hosting Supabase.

### Using the Resend Integration

Resend includes a pre-built integration with Supabase. Connecting Resend as your email provider will allow you to send your Supabase emails (e.g., password resets, email confirmations) through Resend.

<YouTube id="BkfDsGMgutk" />

<Steps>
  <Step title="Navigate to the Integrations Settings Dashboard page." />

  <Step title="Connect your account to Supabase.">
    Click **Connect to Supabase** and login to your Supabase account if prompted.

    <img alt="Resend Integrations settings" src="https://mintcdn.com/resend/_kGPo-rF0-rO9nI4/images/resend-integrations-settings.png?fit=max&auto=format&n=_kGPo-rF0-rO9nI4&q=85&s=b954067bfb28d84f7d8201e05a449815" width="3024" height="1900" data-path="images/resend-integrations-settings.png" />
  </Step>

  <Step title="Add your API key.">
    Select a project and click **Select Project**, then select your domain and click **Add API Key**. Resend will create an API key for you. Add a sender name and click **Configure SMTP Integration**.

    <img alt="Resend Integrations settings" src="https://mintcdn.com/resend/_kGPo-rF0-rO9nI4/images/resend-supabase-setup-smtp.png?fit=max&auto=format&n=_kGPo-rF0-rO9nI4&q=85&s=e744247952bc105d6083babcc315b0a6" width="3024" height="1900" data-path="images/resend-supabase-setup-smtp.png" />
  </Step>

  <Step title="Confirm the integration.">
    Click on **Supabase Dashboard** to confirm the integration.

    <img alt="Resend Integrations settings" src="https://mintcdn.com/resend/_kGPo-rF0-rO9nI4/images/resend-supabase-setup-confirm.png?fit=max&auto=format&n=_kGPo-rF0-rO9nI4&q=85&s=d72c13ba50f60530587107b6d7040223" width="1360" height="150" data-path="images/resend-supabase-setup-confirm.png" />
  </Step>
</Steps>

<Info>
  Supabase has a rate limit on the number of emails you can send per hour and
  requires you to [connect a custom email provider for more than 2
  emails/hour](https://supabase.com/docs/guides/auth/rate-limits). Once you set
  Resend as your email provider, you can send additional emails (by default, 25
  emails/hour, although you can change the rate limit in your project's
  [authentication
  settings](https://supabase.com/docs/guides/deployment/going-into-prod#rate-limiting-resource-allocation--abuse-prevention)).
</Info>

### Custom Auth Functions

Benefit of using custom auth functions:

* More control over the email sending process since you control the sending function.
* More control over the email template using React Email or Resend Templates.

Note that this requires enabling [Supabase Auth Hooks](https://supabase.com/docs/guides/auth/auth-hooks).

<YouTube id="tB_HcKjW8fQ" />

<Card title="Supabase Auth Hooks with Resend Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/supabase-auth-hooks-with-resend-templates">
  See the full source code.
</Card>

### Self-hosted with Custom SMTP

If you're self-hosting Supabase, you can use a custom SMTP server to send your emails. [Learn more here](/docs/send-with-smtp).

## Send Emails with Supabase Edge Functions

If you're using Supabase Edge Functions, you can add email sending to your function by using the Resend Node.js SDK. You can use these functions for Auth Emails ([as shown above](#custom-auth-functions)) or for other emails (e.g., app notifications, account activity).

First, make sure you have the latest version of the [Supabase CLI](https://supabase.com/docs/guides/cli#installation) installed.

<Steps>
  <Step title="Create Supabase function">
    Create a new function locally:

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    supabase functions new resend
    ```
  </Step>

  <Step title="Edit the handler function">
    Paste the following code into the `index.ts` file:

    ```js index.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    import { serve } from "https://deno.land/std@0.168.0/http/server.ts";

    const RESEND_API_KEY = 're_xxxxxxxxx';

    const handler = async (_request: Request): Promise<Response> => {
        const res = await fetch('https://api.resend.com/emails', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': `Bearer ${RESEND_API_KEY}`
            },
            body: JSON.stringify({
                from: 'Acme <onboarding@resend.dev>',
                to: ['delivered@resend.dev'],
                subject: 'hello world',
                html: '<strong>it works!</strong>',
            })
        });

        const data = await res.json();

        return new Response(JSON.stringify(data), {
            status: 200,
            headers: {
                'Content-Type': 'application/json',
            },
        });
    };

    serve(handler);
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

    <Card title="Supabase Edge Functions Example" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-supabase-edge-functions-example">
      See the full source code.
    </Card>
  </Step>
</Steps>

## Get more help

If you have any questions, please let us know at [support@resend.com](mailto:support@resend.com).
