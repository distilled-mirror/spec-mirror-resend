> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Vercel Marketplace Integration

> Create and connect a Resend account directly from Vercel using the dashboard or the CLI.

The Resend integration on the [Vercel Marketplace](https://vercel.com/marketplace/resend) lets you provision a Resend account without leaving Vercel. Once installed, Vercel connects the account to your project so you can start sending email right away.

## What you get

* A Resend account created and linked to your Vercel account.
* A connection between that account and the Vercel project you selected.
* Access to the full [Resend dashboard](https://resend.com), where you can add domains, manage API keys, and view logs.

## Prerequisites

Before you begin, make sure you have the following:

* A Vercel account with a project.
* A domain purchased in Vercel.

## Two surfaces

You can add Resend to a Vercel project from any of these surfaces:

* [**Vercel Dashboard**](#vercel-dashboard)
* [**Vercel CLI**](#vercel-cli)

<video src="https://mintcdn.com/resend/ZwOiKeN1JKyNwVEm/images/vercel-marketplace-integration.mp4?fit=max&auto=format&n=ZwOiKeN1JKyNwVEm&q=85&s=b315655682855d90ee08da4ca61d6b4a" autoPlay muted loop playsInline aria-label="Demonstration of installing Resend from the Vercel Marketplace" className="w-full aspect-video" data-path="images/vercel-marketplace-integration.mp4" />

### Vercel Dashboard

To install Resend from the Vercel Marketplace:

1. Log in to Vercel and go to the [Marketplace](https://vercel.com/resend/~/integrations/marketplace).
2. Search for "Resend" and click on the integration card.
3. Click on the "Install" button.
4. To create a new Resend account for your Vercel project, click on the "Create Account" option and **Continue**.
5. Click **Accept and Create** to continue the installation.
6. Select your custom domain associated with your Vercel project (or purchase a domain from Vercel).
7. Select the region your emails will be sent from (defaults to North Virginia).
8. Select a plan (free or paid).
9. Click **Continue** and **Create** to complete the installation.
10. Select your Vercel project to connect the domain to Resend and click **Connect**.

Vercel creates a new Resend account for your Vercel project, connects the domain to Resend, and provisions an API key.

### Vercel CLI

Add Resend to the linked project from your terminal. With the [Vercel CLI](https://vercel.com/docs/cli) installed:

1. Run `vc i resend -m domain=example.com`. To choose the region your emails will be sent from, pass it as metadata: `-m region=eu-west-1` (defaults to `us-east-1`). Supported regions: `us-east-1`, `eu-west-1`, `sa-east-1`, and `ap-northeast-1`.
2. Select your custom domain associated with your Vercel project (or purchase a domain from Vercel).
3. Select a plan (free or paid).
4. Click **Continue** and **Create** to complete the installation.
5. Select your Vercel project to connect the domain to Resend and click **Connect**.
6. Click **Complete onboarding** to view the domain in your new Resend account.
7. Click **Auto configure** to automatically add the DNS records to your Vercel domain.

Get more help adding a custom domain in [Resend's documentation](/docs/dashboard/domains/introduction).

## Billing

Accounts created from the Marketplace are billed by Vercel. Manage your account from the Vercel installation dashboard.

<Warning>
  Discounts, promo codes, and startup or partner credits do not apply to
  Marketplace plans.
</Warning>

## Next steps

* Send your first email with [Next.js](/docs/send-with-nextjs).
* Explore [receiving emails](/docs/dashboard/receiving/introduction) with Resend.
* Use Resend [Templates](/docs/dashboard/templates/introduction) to simplify your email sending and design.
* Create your first Resend [Automation](/docs/dashboard/automations/introduction).
