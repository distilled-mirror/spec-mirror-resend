> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Lovable and Resend

> Learn how to add the Resend integration to your Lovable project.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

[Lovable](https://lovable.dev) is a platform for building web sites, tools, apps, and projects via chat. You can add Resend in a Lovable project by asking the chat to add email sending with Resend.

If you prefer to watch a video, check out our video walkthrough below.

<YouTube id="0gw693uZt0w" />

## Guide

<Steps>
  <Step title="Add your Resend API key">
    To use Resend with Lovable, you'll need to add a Resend API key, which you can create in the [Resend Dashboard](https://resend.com/api-keys). Do not share your API key with others or expose it in the browser or other client-side code.

    Lovable may integrate Resend in a few different ways:

    * Use the Supabase integration to store the API key **(highly recommended)**
    * Ask users to provide their own API key
    * Add the API key directly in the code

    You may need to prompt Lovable to store the API key for Resend using Supabase. Clicking **Add API key** will open a modal where you can add the API key.

    <img src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/lovable-integration.png?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=c071ba3ae671bc6cafd8dfd43e12772d" alt="adding the Resend integration to a Lovable chat" width="2992" height="1868" data-path="images/lovable-integration.png" />

    <Info>
      At the time of writing, Lovable does not securely handle API keys
      independently. Instead, it uses the [Supabase integration to store
      secrets](https://docs.lovable.dev/integrations/supabase#storing-secrets-api-keys-%26-config).
    </Info>
  </Step>

  <Step title="Add a custom domain to your Resend account">
    By default, you can only send emails to your own email address.

    To send emails to other email addresses:

    1. Add a [custom domain to your Resend account](/docs/add-a-domain).
    2. Add the custom domain to the `from` field in the `resend` function in Lovable (or ask the chat to update these fields).

    <Info>
      By default, Lovable deploys using the test domain `resend.dev`. Once your custom domain is verified, the function does not automatically redeploy or update the sender address.

      You’ll need to ask Lovable to manually update the `From` email to use your verified domain and then redeploy the function so the changes take effect.
    </Info>

    Get more help adding a custom domain in [Resend's documentation](/docs/dashboard/domains/introduction).
  </Step>
</Steps>
