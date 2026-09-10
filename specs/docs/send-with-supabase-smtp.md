> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Supabase with SMTP

> Learn how to integrate Supabase Auth with Resend SMTP.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Get the Resend SMTP credentials">
    When configuring your SMTP integration, you'll need to use the following credentials:

    * **Host**: `smtp.resend.com`
    * **Port**: `465`
    * **Username**: `resend`
    * **Password**: `YOUR_API_KEY`
  </Step>

  <Step title="Integrate with Supabase SMTP">
    After logging into your Supabase account, you'll need to enable the SMTP integration.

    1. Go to your Supabase project
    2. Click on **Authentication** in the left sidebar
    3. Click **Email** under the **Notifications** section
    4. Click **SMTP Settings**
    5. Add your Sender email and name (these are required fields). For example: `support@example.com` and `ACME Support`.

    <img alt="Supabase Auth - SMTP Sender email and name settings" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/supabase-auth-smtp-sender-email-name.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=1db59a322b21efb38bc298a5796d32b3" width="2080" height="618" data-path="images/supabase-auth-smtp-sender-email-name.png" />

    6. You can copy-and-paste the [SMTP credentials](https://resend.com/settings/smtp) from Resend to Supabase.

    <img alt="Supabase Auth - SMTP Settings" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/supabase-auth-smtp-settings.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=70c068d96e4f03c7e2f03b6e71219d4f" width="2076" height="1536" data-path="images/supabase-auth-smtp-settings.png" />

    After that, you can click the **Save** button and all of your emails will be sent through Resend.
  </Step>
</Steps>
