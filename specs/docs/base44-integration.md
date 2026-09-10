> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Base44 and Resend

> Learn how to add the Resend integration to your Base44 project.

[Base44](https://base44.com/) is a platform for building apps with AI. You can add Resend in a Base44 project by asking the chat to add email sending with Resend.

<Info>
  This integration requires backend functions, a feature available only on
  Builder tier and above. Learn more about [Base44
  pricing](https://base44.com/pricing).
</Info>

## Guide

<Steps>
  <Step title="Add the Resend integration in Base44">
    **If starting a new app:**

    1. Click **Integration** in the top nav.
    2. Search for **Resend**, select it, and choose **Use This Integration**.

    <img alt="Resend Integration page" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/base44-integration.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=f98f8dda5a22d0a0aa0aadc40c9324f3" width="1024" height="475" data-path="images/base44-integration.png" />

    **If adding Resend to an existing app:**

    1. Enable backend functions.
    2. Ask the chat: "Add the Resend email integration to my app. Prompt me to provide the API key and send a welcome email to new users."

    <Note>
      See the [Base44
      documenation](https://docs.base44.com/Integrations/Resend-integration) for
      more information.
    </Note>
  </Step>

  <Step title="Add your Resend API key">
    However you add Resend to your project, you'll need to add a Resend API key, which you can create in the [Resend Dashboard](https://resend.com/api-keys). Do not share your API key with others or expose it in the browser or other client-side code.

    Copy the API key and paste it into the **RESEND\_API\_KEY** field in Base44.

    <img src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/base44-integration-1.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=e10a7a52b06dde106b7a2db585bb7b30" alt="Adding your Resend API key to Base44" width="1024" height="476" data-path="images/base44-integration-1.png" />
  </Step>

  <Step title="Add a custom domain to your Resend account">
    By default, you can only send emails to your own email address.

    To send emails to other email addresses:

    1. Add a [custom domain to your Resend account](/docs/add-a-domain).
    2. Add the custom domain to the `from` field in the `resend` function in the Base44 backend function (or ask the chat to update these fields).

    Get more help adding a custom domain in [Resend's documentation](/docs/dashboard/domains/introduction).
  </Step>
</Steps>
