> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Better Auth emails with Resend

> Learn how to send Better Auth transactional emails through Resend using email hooks.

[Better Auth](https://better-auth.com) is a framework-agnostic authentication library for TypeScript. It relies on transactional email for password resets, email verification, magic links, and one-time codes, all of which you can deliver with Resend.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)
* A project with [Better Auth installed](https://better-auth.com/docs/installation)

## Install the Resend SDK

<CodeGroup>
  ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
  npm install resend
  ```

  ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
  pnpm add resend
  ```

  ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
  yarn add resend
  ```
</CodeGroup>

Add your API key to the environment:

```bash .env theme={"theme":{"light":"github-light","dark":"vesper"}}
RESEND_API_KEY=re_xxxxxxxxx
```

<Note>
  The hook examples below call `void resend.emails.send(...)` instead of
  awaiting it, [as Better Auth
  recommends](https://better-auth.com/docs/concepts/email), so the response time
  doesn't reveal whether an account exists. On serverless platforms, wrap the
  send in `waitUntil` (or your platform's equivalent) so the function doesn't
  terminate before the email is sent.
</Note>

## Send password reset and verification emails

Better Auth calls your `sendResetPassword` and `sendVerificationEmail` hooks when a user requests a reset or needs to confirm their address. Send the email with Resend inside each hook.

```typescript auth.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import { betterAuth } from 'better-auth';
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

export const auth = betterAuth({
  emailAndPassword: {
    enabled: true,
    sendResetPassword: ({ user, url }) => {
      void resend.emails.send({
        from: 'Acme <onboarding@example.com>',
        to: user.email,
        subject: 'Reset your password',
        html: `Click <a href="${url}">here</a> to reset your password.`,
      });
    },
  },
  emailVerification: {
    sendVerificationEmail: ({ user, url }) => {
      void resend.emails.send({
        from: 'Acme <onboarding@example.com>',
        to: user.email,
        subject: 'Verify your email address',
        html: `Click <a href="${url}">here</a> to verify your email.`,
      });
    },
  },
});
```

<Info>
  Set the `from` address to match your [verified domain](/docs/add-a-domain).
</Info>

## Send magic links (optional)

If you use the [magic link plugin](https://better-auth.com/docs/plugins/magic-link), send the sign-in link through the `sendMagicLink` hook.

```typescript auth.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import { betterAuth } from 'better-auth';
import { magicLink } from 'better-auth/plugins';
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

export const auth = betterAuth({
  plugins: [
    magicLink({
      sendMagicLink: ({ email, url }) => {
        void resend.emails.send({
          from: 'Acme <onboarding@example.com>',
          to: email,
          subject: 'Sign in to Acme',
          html: `Click <a href="${url}">here</a> to sign in.`,
        });
      },
    }),
  ],
});
```

<Info>
  Set the `from` address to match your [verified domain](/docs/add-a-domain).
</Info>

## Send one-time codes (optional)

The [email OTP plugin](https://better-auth.com/docs/plugins/email-otp) sends a one-time password (OTP), a numeric code, instead of a link. The `type` argument tells you which flow triggered the request so you can tailor the subject line.

```typescript auth.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import { betterAuth } from 'better-auth';
import { emailOTP } from 'better-auth/plugins';
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

export const auth = betterAuth({
  plugins: [
    emailOTP({
      sendVerificationOTP: ({ email, otp, type }) => {
        void resend.emails.send({
          from: 'Acme <onboarding@example.com>',
          to: email,
          subject:
            type === 'sign-in' ? 'Your sign-in code' : 'Your verification code',
          html: `Your code is <strong>${otp}</strong>.`,
        });
      },
    }),
  ],
});
```

<Info>
  Set the `from` address to match your [verified domain](/docs/add-a-domain).
</Info>

## Customize email templates

For richer, reusable emails, author your templates with [React Email](https://react.email) and pass the rendered component to Resend's `react` field, or reference a [Resend template](/docs/dashboard/templates/introduction) by `id`.

```typescript auth.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import { ResetPasswordEmail } from './emails/reset-password';

sendResetPassword: ({ user, url }) => {
  void resend.emails.send({
    from: 'Acme <onboarding@example.com>',
    to: user.email,
    subject: 'Reset your password',
    react: ResetPasswordEmail({ url }),
  });
},
```

<Info>
  Set the `from` address to match your [verified domain](/docs/add-a-domain).
</Info>

## Debugging email delivery

When a flow doesn't behave as expected, check both sides:

* **Better Auth logs** show the hook invocation and any errors thrown while sending.
* [**Resend Logs**](https://resend.com/logs) show the delivery side: accepted, delivered, opened, bounced.

Together, you get end-to-end visibility across the entire delivery chain.
