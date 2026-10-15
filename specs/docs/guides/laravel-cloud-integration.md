> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Laravel Cloud Integration

> Connect a Resend account to Laravel Cloud and send email from your environments.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

[Laravel Cloud](https://laravel.com/cloud) hosts Laravel applications and manages Resend as an email resource. Connect a Resend account once for your organization, then attach email to any environment. Laravel Cloud creates a sending key and injects the mail variables your application needs.

## What you get

* OAuth connection to your Laravel Cloud organization.
* Resource you can reuse across environments.
* A sending key for each environment, injected as environment variables.
* Billing that stays on your [Resend plan](/docs/dashboard/settings/billing).

## Prerequisites

* A Laravel Cloud organization with an environment.
* A Resend account with a [verified domain](/docs/add-a-domain).

## Connect your Resend account

Connect from the organization settings, or the first time you attach email to an environment. Either path sends you to Resend to approve access.

Prefer a video walkthrough?

<YouTube id="LuoW0h0tDOk" />

<Steps>
  <Step title="Open the canvas">
    Open the environment canvas and choose the **Email** resource.
  </Step>

  <Step title="Approve full access">
    On the Resend consent screen, pick the team Laravel Cloud should use and choose **Full access**. Laravel Cloud returns you to the same environment and imports the sending domains already on that team.

    <Info>
      **Full access** lets Laravel Cloud import your existing domains and set up the
      webhooks it needs. **Sending access** can only send email, so Laravel Cloud
      can't finish setup with that permission.
    </Info>

    <video src="https://mintcdn.com/resend/N1PEHIWHV2KtNePv/images/laravel-cloud-integration-1.mp4?fit=max&auto=format&n=N1PEHIWHV2KtNePv&q=85&s=e5245e8aa3da5fc711fc983b6efdbfbb" autoPlay muted loop playsInline aria-label="Connecting a Resend account from the Laravel Cloud canvas" className="w-full aspect-video" data-path="images/laravel-cloud-integration-1.mp4" />
  </Step>

  <Step title="Connect a domain and create a key">
    Select a verified domain or create a new one. Click **Continue**.

    <video src="https://mintcdn.com/resend/N1PEHIWHV2KtNePv/images/laravel-cloud-integration-2.mp4?fit=max&auto=format&n=N1PEHIWHV2KtNePv&q=85&s=f360a14b67e7f91ccb3131b2073c6ea2" autoPlay muted loop playsInline aria-label="Choosing a sending domain, sender, and key, then attaching email to a Laravel Cloud environment" className="w-full aspect-video" data-path="images/laravel-cloud-integration-2.mp4" />

    Enter the sender address and sender name, then choose a sending key.

    * **Create a new key** creates a full access key used by this environment.
    * **Reuse existing key** shares a key already used by another environment in the organization.

    Confirm and attach email to finish.
  </Step>

  <Step title="Redeploy your application">
    For changes to take effect, redeploy your application.
  </Step>
</Steps>

Connecting and disconnecting requires the **Edit organization integrations** permission. See [roles and permissions](https://laravel.com/cloud/docs/rbac) for more details.

### Injected environment variables

```ini theme={"theme":{"light":"github-light","dark":"vesper"}}
RESEND_API_KEY=re_xxxxxxxxxxxx
MAIL_MAILER=resend
MAIL_FROM_ADDRESS=hello@notifications.example.com
MAIL_FROM_NAME="Your application name"
```

`MAIL_FROM_ADDRESS` and `MAIL_FROM_NAME` use the sender you entered. Laravel Cloud encrypts `RESEND_API_KEY` and masks it, the same way it handles a database password.

A custom environment variable with the same name takes priority over an injected one. Define the custom variable, then deploy. See [Laravel Cloud's environment variables documentation](https://laravel.com/cloud/docs/environments#environment-variables) for how overrides work.

To send from your own machine, copy these variables into your local `.env`. Laravel Cloud injects them into the hosted environment.

## Send from your application

### Laravel

[Laravel ships with a Resend mail transport](https://laravel.com/cloud/docs/resources/email#laravel). The transport needs Resend's PHP SDK. If the package is missing, Laravel Cloud prompts you to add it to the project's dependencies:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
composer require resend/resend-php
```

Laravel reads the injected variables directly, so no further configuration is required. Send mail as you normally would:

```php theme={"theme":{"light":"github-light","dark":"vesper"}}
use Illuminate\Support\Facades\Mail;

Mail::to($user)->send(new OrderShipped($order));
```

The key has full access, so the same application can call the rest of the Resend API. Install [`resend/resend-laravel`](/docs/send-with-laravel) for the Laravel SDK, or send over [SMTP](/docs/send-with-laravel-smtp).

### Other frameworks

Laravel Cloud injects `RESEND_API_KEY` for every runtime. Read the key from the environment and pass it to the [API](/docs/api-reference/introduction) or an [SDK](/docs/sdks).

<Note>
  Queued mail can fail as a failed job. [Laravel
  Nightwatch](https://nightwatch.laravel.com) traces those jobs and alerts you
  when they start failing.
</Note>

## Attach Resend with the API

[Attach Resend to an environment](https://laravel.com/cloud/docs/api/email/attach-resend-to-environment#attach-resend-to-environment) with a bearer token from the Laravel Cloud UI. `from_address` and `from_name` are required. Set `key_strategy` to `create` for a new key, or `reuse` and pass `reuse_key_id` to share a key another environment already uses. `key_name` is optional.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
curl --request POST \
  --url https://cloud.laravel.com/api/environments/{environment}/resend \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{
  "from_address": "hello@notifications.example.com",
  "from_name": "Acme",
  "key_name": "production",
  "key_strategy": "create"
}'
```

Deploy the environment after the request so the application receives the mail variables.

The same API can list what you attach and change it later:

* [List sending domains](https://laravel.com/cloud/docs/api/email/list-sending-domains) for the organization.
* [List reusable sending keys](https://laravel.com/cloud/docs/api/email/list-reusable-sending-keys) that other environments can share.
* [Update the sender](https://laravel.com/cloud/docs/api/email/update-environment-resend-sender) with `from_address` and `from_name`.
* [Detach Resend](https://laravel.com/cloud/docs/api/email/detach-resend-from-environment). This deletes the environment's sending key unless another environment shares it.

## Next steps

* Send your first email with [Laravel](/docs/send-with-laravel).
* Add and verify a [domain](/docs/dashboard/domains/introduction).
* Design messages with [Templates](/docs/dashboard/templates/introduction).
* Follow up with an [Automation](/docs/dashboard/automations/introduction).
