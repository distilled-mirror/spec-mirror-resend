> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Leap and Resend

> Learn how to add the Resend integration to your Leap.new project.

[Leap](https://leap.new) is a platform for building full-stack web and mobile apps via chat.

## Guide

<Steps>
  <Step title="Ask Leap to add Resend">
    You can add Resend in a Leap project by asking the chat to add email sending with Resend.

    **Example prompt**

    ```
    When someone fills out the contact form, send an email using Resend.
    ```
  </Step>

  <Step title="Add your Resend API key">
    To use Resend with Leap, you'll need to add a Resend API key, which you can create in the [Resend Dashboard](https://resend.com/api-keys). Do not share your API key with others or expose it in the browser or other client-side code.

    Leap will prompt you to set a secret value on the Infrastructure page. Paste your key value and click **Update secret**.

    <img src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/leap-new-integration.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=d1c68aa7b6144ffcd8ee2793cdebe67d" alt="adding the Resend integration to a leap.new chat" width="3360" height="2100" data-path="images/leap-new-integration.png" />

    <Info>
      Learn more about the Resend integration in the [Leap
      documentation](https://docs.leap.new/integrations/resend).
    </Info>
  </Step>

  <Step title="Add a custom domain to your Resend account">
    By default, you can only send emails to your own email address.

    To send emails to other email addresses:

    1. Add a [custom domain to your Resend account](/docs/add-a-domain).
    2. Add the custom domain to the `from` field in the `resend` function in Leap (or ask the chat to update these fields).

    Get more help adding a custom domain in [Resend's documentation](/docs/dashboard/domains/introduction).
  </Step>
</Steps>
