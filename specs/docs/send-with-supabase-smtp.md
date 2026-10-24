> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Supabase with SMTP

> Learn how to integrate Supabase Auth with Resend SMTP.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

## Guide

**1. Get the Resend SMTP credentials**

When configuring your SMTP integration, you'll need to use the following credentials:

* **Host**: `smtp.resend.com`
* **Port**: `465`
* **Username**: `resend`
* **Password**: `YOUR_API_KEY`

**2. Integrate with Supabase SMTP**

After logging into your Supabase account, you'll need to enable the SMTP integration.

1. Go to your Supabase project
2. Click on **Authentication** in the left sidebar
3. Click **Email** under the **Notifications** section
4. Click **SMTP Settings**
5. Add your Sender email and name (these are required fields). For example: `support@example.com` and `ACME Support`.

![Supabase Auth - SMTP Sender email and name settings](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/supabase-auth-smtp-sender-email-name.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=1db59a322b21efb38bc298a5796d32b3)

6. You can copy-and-paste the [SMTP credentials](https://resend.com/settings/smtp) from Resend to Supabase.

![Supabase Auth - SMTP Settings](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/supabase-auth-smtp-settings.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=70c068d96e4f03c7e2f03b6e71219d4f)

After that, you can click the **Save** button and all of your emails will be sent through Resend.
