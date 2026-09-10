> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Auth0 transactional emails with Resend

> Learn how to send Auth0 transactional emails through Resend using the official integration.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

[Auth0](https://auth0.com) supports Resend as a built-in email provider. Authentication flows depend on reliable delivery for verification codes, password resets, and other crucial emails.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

Prefer a video walkthrough?

<YouTube id="-xlz8xVN3Rc" />

## Set up the Resend provider in Auth0

In the Auth0 Dashboard, go to **Branding > Email Provider**, toggle on **Use my own email provider**, and select **Resend**.

Enter your API key and set the **From** address to match your verified domain. Click **Save** to apply the changes.

<img src="https://mintcdn.com/resend/3aaPXnVunyH4ynzk/images/auth0-setup.png?fit=max&auto=format&n=3aaPXnVunyH4ynzk&q=85&s=1e7ff74e83ff205e0b499c5aacdb7d3f" alt="Auth0 Resend Integration" className="extraWidth" width="2220" height="970" data-path="images/auth0-setup.png" />

To test that it's working, click **Send Test Email**. The email will appear in your Resend dashboard and email inbox.

<Info>
  For the full setup guide, see the [Auth0
  documentation](https://auth0.com/docs/customize/email/smtp-email-providers/resend).
</Info>

## Send emails with Auth0 Actions (optional)

For more control over delivery, like per-organization sender addresses, conditional routing, or custom logic, you can use an Auth0 Action instead.

In the Auth0 Dashboard, go to **Actions > Library**, create a new Custom action.

<img src="https://mintcdn.com/resend/3aaPXnVunyH4ynzk/images/auth0-action.png?fit=max&auto=format&n=3aaPXnVunyH4ynzk&q=85&s=6eec4f5953cfa2a5e7848b8dfbe184a0" alt="Auth0 Custom Action" className="extraWidth" width="2264" height="706" data-path="images/auth0-action.png" />

To enable Resend in the Action:

1. Add `resend` as a dependency.
   <img src="https://mintcdn.com/resend/3aaPXnVunyH4ynzk/images/auth0-dependency.png?fit=max&auto=format&n=3aaPXnVunyH4ynzk&q=85&s=7789456d3dd2c52559961357226cea0a" alt="Auth0 Custom Action" width="1852" height="973" data-path="images/auth0-dependency.png" />
2. Store your API key as a secret named `RESEND_API_KEY`.
   <img src="https://mintcdn.com/resend/3aaPXnVunyH4ynzk/images/auth0-secret.png?fit=max&auto=format&n=3aaPXnVunyH4ynzk&q=85&s=6326f23f2690292e87545282c1fee855" alt="Auth0 Custom Action" width="1822" height="869" data-path="images/auth0-secret.png" />

Here's a working example that sends a security alert on first login:

```javascript theme={"theme":{"light":"github-light","dark":"vesper"}}
const { Resend } = require('resend');

exports.onExecutePostLogin = async (event, api) => {
  const resend = new Resend(event.secrets.RESEND_API_KEY);

  if (event.stats.logins_count === 1) {
    await resend.emails.send({
      from: 'Security <security@example.com>',
      to: event.user.email,
      subject: 'New login detected',
      html: `<p>Hi ${event.user.name}, a new login was detected from ${event.request.ip}.</p>`,
    });
  }
};
```

Deploy it by adding the action to the **Post Login** trigger under **Actions > Triggers**.

## Customize Email Templates

To customize the email templates that Auth0 sends out, go to **Branding > Email Templates** in the Auth0 Dashboard and make your changes to the existing templates.

For more advanced templating, consider either [React Email](#react-email) or [Resend Templates](#resend-templates).

### React Email

Auth0 email templates use Liquid syntax for dynamic variables like `{{ user.email }}` and `{{ url }}`. You can author templates with [React Email](https://react.email) and inject Liquid variables before pasting the rendered HTML into Auth0.

Define your Liquid variables as constants to avoid HTML encoding issues during rendering:

```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
export const VARIABLES = {
  url: '{{ url }}',
  user: { email: '{{ user.email }}' },
  application: { name: '{{ application.name }}' },
};
```

Use them in your React Email components, render to static HTML, and paste the output into **Branding > Email Templates** in Auth0.

### Resend Templates

To use Resend templates with Auth0, define your templates in the [Resend Dashboard](https://resend.com/templates) and reference them in your [Custom OAuth Actions](#send-emails-with-auth0-actions-optional).

For instance, the following code uses a Resend template with the id of `login-detected` that contains two variables (`first_name` and `ip_address`) to be passed in the call. [Learn more about Resend templates](/docs/dashboard/templates/introduction).

```javascript theme={"theme":{"light":"github-light","dark":"vesper"}}
const { Resend } = require('resend');

exports.onExecutePostLogin = async (event, api) => {
  const resend = new Resend(event.secrets.RESEND_API_KEY);

  if (event.stats.logins_count === 1) {
    await resend.emails.send({
      from: 'Security <security@example.com>',
      to: event.user.email,
      template: {
        id: 'login-detected',
        variables: {
          first_name: event.user.name,
          ip_address: event.request.ip,
        },
      },
    });
  }
};
```

## Debugging Email Delivery

When something goes wrong, it's helpful to see detailed logs across both sides:

* **Auth0 Logs** (**Monitoring > Logs**) shows send events and any errors raised from the Resend integration.
* [**Resend Logs**](https://resend.com/logs) show the delivery side: accepted, delivered, opened, bounced.

Together, you get end-to-end visibility across the entire delivery chain.
