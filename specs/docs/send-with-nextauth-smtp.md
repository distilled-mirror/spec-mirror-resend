> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using NextAuth with SMTP

> Learn how to send your first email using NextAuth.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Install the [NextAuth](https://next-auth.js.org/getting-started/example#install-nextauth) package.

    <CodeGroup>
      ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
      npm install next-auth
      ```

      ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
      yarn add next-auth
      ```

      ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
      pnpm add next-auth
      ```

      ```bash bun theme={"theme":{"light":"github-light","dark":"vesper"}}
      bun add next-auth
      ```
    </CodeGroup>

    Then, install the [Nodemailer](https://www.npmjs.com/package/nodemailer) package.

    <CodeGroup>
      ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
      npm install nodemailer
      ```

      ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
      yarn add nodemailer
      ```

      ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
      pnpm add nodemailer
      ```

      ```bash bun theme={"theme":{"light":"github-light","dark":"vesper"}}
      bun add nodemailer
      ```
    </CodeGroup>
  </Step>

  <Step title="Configure SMTP credentials">
    Add your Resend SMTP crendentials in your application's `.env` file:

    ```ini .env theme={"theme":{"light":"github-light","dark":"vesper"}}
    EMAIL_SERVER_USER=resend
    EMAIL_SERVER_PASSWORD=YOUR_API_KEY
    EMAIL_SERVER_HOST=smtp.resend.com
    EMAIL_SERVER_PORT=465
    EMAIL_FROM=onboarding@resend.dev
    ```
  </Step>

  <Step title="Configure Email Provider">
    Finally, in your \[...nextauth].js file (typically located in pages/api/auth), configure the Email provider with your SMTP settings:

    ```js index.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    import NextAuth from 'next-auth';
    import EmailProvider from 'next-auth/providers/email';
    import nodemailer from 'nodemailer';

    export default NextAuth({
      providers: [
        EmailProvider({
          server: {
            host: process.env.EMAIL_SERVER_HOST,
            port: process.env.EMAIL_SERVER_PORT,
            auth: {
              user: process.env.EMAIL_SERVER_USER,
              pass: process.env.EMAIL_SERVER_PASSWORD,
            },
          },
          from: process.env.EMAIL_FROM,
        }),
        // ... other providers as needed
      ],
      // ... any other NextAuth.js configs
    });
    ```
  </Step>
</Steps>
