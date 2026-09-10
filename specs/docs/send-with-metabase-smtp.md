> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Metabase with SMTP

> Learn how to integrate Metabase with Resend SMTP.

### Prerequisites

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

  <Step title="Integrate with Metabase SMTP">
    After logging into your [Metabase Cloud](https://www.metabase.com/cloud/login) account, you’ll need to enable the SMTP integration.

    1. From your Metabase Cloud Admin Panel, go to **Settings > Email** in the left menu. You'll see the form below.

    <img alt="Metabase Cloud SMTP" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/metabase-smtp-1.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=b11a45255f8f9058f03cebbd604eb4e5" width="1488" height="1352" data-path="images/metabase-smtp-1.png" />

    2. Copy-and-paste the SMTP credentials from Resend to Metabase Cloud. Finally, click the **Save** button and all of your emails will be sent through Resend.

    <img alt="Metabase Cloud SMTP" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/metabase-smtp-2.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=ca2550e6061a992cc3c9a345eacd4c39" width="3600" height="2250" data-path="images/metabase-smtp-2.png" />
  </Step>
</Steps>
