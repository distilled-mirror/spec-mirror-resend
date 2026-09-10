> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Customer.io with SMTP

> Learn how to integrate Customer.io with Resend SMTP.

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

  <Step title="Integrate with Customer.io SMTP">
    After logging into your [Customer.io](https://customer.io) account, you'll need to enable the SMTP integration.

    1. Go to **Settings** > **Workspace Settings**.

    <img alt="Customer.io SMTP - Workspace Settings" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/customer-io-smtp-1.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=97d3402e7acb7c66e5d54ff2886dd4e3" width="3414" height="1886" data-path="images/customer-io-smtp-1.png" />

    2. Go to the Messaging tab and select **Email**.

    <img alt="Customer.io SMTP - Email" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/customer-io-smtp-2.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=af35d8a9c99681e1a508694f02157943" width="3414" height="1886" data-path="images/customer-io-smtp-2.png" />

    3. Select the **Custom SMTP** tab and click **Add Custom SMTP Server**.

    <img alt="Customer.io SMTP - Add Custom SMTP Server" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/customer-io-smtp-3.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=1d18082018463dc5989fb91d8f881b39" width="3414" height="1886" data-path="images/customer-io-smtp-3.png" />

    4. Select **Other SMTP** and click **Continue to set up**.

    <img alt="Customer.io SMTP - Other SMTP" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/customer-io-smtp-4.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=acc404b8b5b7fc11db0279d84453cb11" width="3414" height="1886" data-path="images/customer-io-smtp-4.png" />

    5. Copy-and-paste the SMTP credentials from Resend to Customer.io.

    <img alt="Customer.io SMTP integration" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/customer-io-smtp-5.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=519742fc4d97d06646fdd52de4f373fd" width="3414" height="1886" data-path="images/customer-io-smtp-5.png" />
  </Step>
</Steps>
