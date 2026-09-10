> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Liferay with SMTP

> Learn how to integrate Liferay with Resend SMTP.

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

  <Step title="Integrate with Liferay">
    After logging into your Liferay instance as the admin user, you'll need to enable the SMTP integration.

    1. Navigate to **Control Panel** → **Server Administration** → **Mail**.

    <img alt="Liferay - SMTP" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/liferay-smtp-1.jpg?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=94e43af6a43bc9fa8ce8cc486eeb4f05" width="1600" height="865" data-path="images/liferay-smtp-1.jpg" />

    2. Copy-and-paste the SMTP credentials from Resend to Liferay.

    * **Outgoing SMTP Server**: `smtp.resend.com`
    * **Outgoing Port**: `465`
    * **Enable StartTLS**: `True`
    * **User Name**: `resend`
    * **Password**: `YOUR_API_KEY`

    Make sure to replace `YOUR_API_KEY` with an existing key or create a new [API Key](https://resend.com/api-keys).

    For the additional JavaMail properties, you can use:

    ```
    mail.smtp.auth=true
    mail.smtp.starttls.enable=true
    mail.smtp.starttls.required=true
    ```
  </Step>
</Steps>
