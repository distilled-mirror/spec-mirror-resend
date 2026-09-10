> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Railway

> Learn how to send your first email using Railway and the Resend Node.js SDK.

[Railway](https://railway.com/?referralCode=resend) enables you to focus on building product instead of managing infrastructure, automatically scaling to support your needs as you grow.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    We've created a [Resend template](https://railway.com/deploy/resend?referralCode=resend\&utm_medium=integration\&utm_source=template\&utm_campaign=generic) using the Resend Node.js SDK as an introduction to using Resend on Railway.

    To get started, you deploy the template to Railway.

    [![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/resend?referralCode=resend\&utm_medium=integration\&utm_source=template\&utm_campaign=generic)

    <img alt="Deploy button highlighted on Railway" src="https://mintcdn.com/resend/UGYfPeFBYurSSqVy/images/send-with-railway.png?fit=max&auto=format&n=UGYfPeFBYurSSqVy&q=85&s=a4b37d9be58e4df72a9eec8e89352e1c" width="1500" height="937" data-path="images/send-with-railway.png" />
  </Step>

  <Step title="Add your API key">
    [Add an API key](https://resend.com/api-keys) from Resend and click **Deploy**.

    <img alt="Template modal with API key field highlighted" src="https://mintcdn.com/resend/UGYfPeFBYurSSqVy/images/send-with-railway-1.png?fit=max&auto=format&n=UGYfPeFBYurSSqVy&q=85&s=0efcfbf778a0193a8c9aa353a07635b6" width="1500" height="897" data-path="images/send-with-railway-1.png" />
  </Step>

  <Step title="Send your first email">
    Once your deployment finishes, click the deploy URL to open the app and send your first email.

    <img alt="Deployment link highlighted" src="https://mintcdn.com/resend/UGYfPeFBYurSSqVy/images/send-with-railway-2.png?fit=max&auto=format&n=UGYfPeFBYurSSqVy&q=85&s=c4a9f0838a4efb406d349c4e815c1c80" width="3360" height="2010" data-path="images/send-with-railway-2.png" />

    While this example uses the [Resend Node.js SDK](https://www.npmjs.com/package/@resend/node), you can add Resend using [any of our Official SDKs](https://resend.com/docs/sdks) that Railway supports.

    <Info>
      Keep in mind that as a basic project, this template sends an email with your
      account each time someone visits your deployment URL, so share the link with
      discretion.
    </Info>

    You can also [set up the project locally](https://docs.railway.com/develop/cli) and make changes to the projectusing the Railway CLI.
  </Step>
</Steps>

## Examples

<Card title="Railway Template" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-node-railway-starter">
  See the full source code.
</Card>
