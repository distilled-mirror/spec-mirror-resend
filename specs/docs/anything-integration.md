> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to add the Resend integration to your Anything project

> Learn how to add the Resend integration to your Anything project.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

[Anything](https://createanything.com) is a platform for building web sites, tools, apps, and projects via chat. With their [Resend integration](https://www.createanything.com/docs/integrations/resend), you can send emails from your Anything project.

If you prefer to watch a video, check out our video walkthrough below.

<YouTube id="Avp1OOMH2Z0" />

## Guide

<Steps>
  <Step title="Call the Resend integration in Anything">
    Type `/Resend` in the chat and select the integration, and ask Anything to add email functionality to your project.

    <img src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/create-xyz-integration.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=810ab7bd912d16365530bbda50d339d8" alt="adding the Resend integration to a Anything chat" width="3360" height="2100" data-path="images/create-xyz-integration.png" />
  </Step>

  <Step title="Add your Resend API key">
    Anything usually prompts you for a Resend API key, which you can add in the [Resend Dashboard](https://resend.com/api-keys). If Anything doesn't prompt you for a Resend API key, click the **More options** <Icon icon="ellipsis-vertical" iconType="solid" /> button and select **Secrets**.

    Click the <Icon icon="plus" iconType="solid" /> **Add new secret** button.

    * **Name:** `RESEND_API_KEY`
    * **Value:** Your Resend API key (e.g., `re_xxxxxxxxx0`)

    Learn more about [Secrets in Create](https://www.createanything.com/docs/essentials#project-settings).
  </Step>

  <Step title="Add a custom domain to your Resend account">
    By default, you can only send emails to your own email address.

    To send emails to other email addresses:

    1. Add a [custom domain to your Resend account](https://resend.com/domains).
    2. Add the custom domain to the `from` field in the `resend` function in Create.

    Learn more about [Functions in Create](https://www.createanything.com/docs/builder/functions).
  </Step>
</Steps>
