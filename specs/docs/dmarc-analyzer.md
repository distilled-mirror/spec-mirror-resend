> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# DMARC Analyzer

> Analyze DMARC XML reports with a free, open-source tool built by Resend.

[DMARC Analyzer](https://github.com/resend/resend-dmarc-analyzer) is an open-source tool built by Resend that parses DMARC XML reports and turns them into human-readable dashboards. You can use it directly in your browser or deploy your own instance to receive automated email digests.

## What is DMARC?

DMARC (Domain-based Message Authentication, Reporting, and Conformance) is an email authentication protocol that builds on [SPF and DKIM](https://resend.com/docs/dashboard/domains/introduction.md). It lets domain owners specify how unauthenticated emails are handled and receive reports about authentication results.

When you [set up a DMARC policy](https://resend.com/docs/dashboard/domains/dmarc.md), mailbox providers send XML reports to the address you specify. These reports contain valuable data about who is sending email on behalf of your domain and whether those emails pass authentication, but the raw XML is difficult to read. The DMARC Analyzer helps you visualize these reports in a human-readable format.

## Features

* Parse and visualize DMARC XML reports instantly
* View SPF and DKIM alignment results per source
* Identify unauthorized senders using your domain
* Self-host with automated report ingestion via [Resend Receiving](https://resend.com/docs/dashboard/receiving/introduction.md)
* Receive email digests summarizing your DMARC reports

> [!NOTE]
>
> For more details on understanding DMARC reports, see our [guide on how to read
> a DMARC report](https://resend.com/blog/how-to-read-a-dmarc-report).

## How to use

### Web interface

The quickest way to get started, with no setup required.

1. Go to [checkdmarc.email](https://checkdmarc.email/)
2. Paste your DMARC XML report (or upload the XML file)
3. View the parsed results instantly

<video src="https://mintcdn.com/resend/IprKFnTRa5k2DXX0/images/dmarc-analyzer.mp4?fit=max&auto=format&n=IprKFnTRa5k2DXX0&q=85&s=eaa56c455d88bc14dfe361a130d0e842" autoPlay muted loop playsInline />

### Self-hosted with automated reports

For ongoing monitoring, deploy your own instance. This connects to Resend Receiving webhooks so DMARC reports sent to your domain are automatically ingested and analyzed, with email digests delivered via Resend.

## Getting started (self-hosted)

**1. Clone the repository**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
git clone https://github.com/resend/resend-dmarc-analyzer.git
cd resend-dmarc-analyzer
```

**2. Install dependencies**

`bash pnpm install ``bash npm install ``bash yarn install ``bash bun install `

**3. Configure environment variables**

Copy the example environment file and fill in the required values:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
cp .env.example .env.local
```

| Variable | Description |
| - | - |
| `RESEND_API_KEY` | Your [Resend API key](https://resend.com/api-keys) |
| `RESEND_WEBHOOK_SECRET` | Signing secret from your [Resend webhook](https://resend.com/webhooks) endpoint set up below |
| `EMAIL_FROM` | Sender address for digest emails (must be from a [verified domain](https://resend.com/domains)) |
| `EMAIL_TO` | Recipient address for digest emails |

**4. Test the application**

Start the development server:

`bash pnpm run dev ``bash npm run dev ``bash yarn run dev ``bash bun run dev `

Register your publicly accessible HTTPS URL in the Resend dashboard and enable the `email.received` event.

* For `rua` reports: `https://example123.ngrok.io/api/webhooks/dmarc/rua`
* For `ruf` report: `https://example123.ngrok.io/api/webhooks/dmarc/ruf`

Copy the signing secret from the webhook details page to the `RESEND_WEBHOOK_SECRET` environment variable.

> [!TIP]
>
> For development, you can create a tunnel to your localhost server using a tool like
> [ngrok](https://ngrok.com/download) or [VS Code Port Forwarding](https://code.visualstudio.com/docs/debugtest/port-forwarding). These tools serve your local dev environment at a public URL you can use to test your local webhook endpoint.
>
> Example: `https://example123.ngrok.io/api/webhook`

**5. Deploy**

Deploy the application to your preferred hosting platform and update the webhook endpoint(s) in the Resend dashboard.

* For `rua` reports: `https://example.com/api/webhooks/dmarc/rua`
* For `ruf` reports: `https://example.com/api/webhooks/dmarc/ruf`

The project is built with [Next.js](https://nextjs.org) so it works with any platform that supports it (e.g., [Vercel](https://vercel.com)).

## Tech stack

DMARC Analyzer is built with [Next.js](https://nextjs.org), [React Email](https://react.email), and [Resend](https://resend.com). The full source code is available on [GitHub](https://github.com/resend/resend-dmarc-analyzer).
