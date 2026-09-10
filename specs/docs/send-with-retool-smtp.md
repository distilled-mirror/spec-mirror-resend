> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Retool with SMTP

> Learn how to integrate Retool with Resend SMTP.

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

  <Step title="Integrate with Retool SMTP">
    Log into your [Retool](https://retool.com) account and create a new SMTP Resource.

    1. Go to **Resources** and click **Create New**

    <img alt="Retool SMTP - Create new Resources" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/retool-smtp-1.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=c6edda6c2512e895bfec5b7e47627d96" width="3025" height="1892" data-path="images/retool-smtp-1.png" />

    2. Search for **SMTP** and select it

    <img alt="Retool SMTP - Search for SMTP" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/retool-smtp-2.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=b95716d79754f6d2f8cedd6522d8e8f8" width="3025" height="1891" data-path="images/retool-smtp-2.png" />

    3. Add name and SMTP credentials

    <img alt="Retool SMTP - Add SMTP credentials" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/retool-smtp-3.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=cbd6221e4b03dfc909f00f966afc4a2a" width="3025" height="1892" data-path="images/retool-smtp-3.png" />
  </Step>
</Steps>
