> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Vercel Marketplace Integration

> Create and connect a Resend account directly from Vercel using the dashboard, the CLI, or v0.

The Resend integration on the [Vercel Marketplace](https://vercel.com/marketplace/resend) lets you provision a Resend account without leaving Vercel. Once installed, Vercel connects the account to your project so you can start sending email right away.

## What you get

* A Resend account created and linked to your Vercel account.
* A connection between that account and the Vercel project you selected.
* Access to the full [Resend dashboard](https://resend.com), where you can add domains, manage API keys, and view logs. Open it with **Open in Resend** from the Resend integration in Vercel.

Marketplace accounts sign in through Vercel and don't have a Resend password.

## Prerequisites

Before you begin, make sure you have the following:

* A Vercel account with a project.
* A domain purchased in Vercel.

## Three surfaces

You can add Resend to a Vercel project from any of these surfaces:

* [**Vercel Dashboard**](#vercel-dashboard)
* [**Vercel CLI**](#vercel-cli)
* [**v0**](#v0)

<video src="https://mintcdn.com/resend/ZwOiKeN1JKyNwVEm/images/vercel-marketplace-integration.mp4?fit=max&auto=format&n=ZwOiKeN1JKyNwVEm&q=85&s=b315655682855d90ee08da4ca61d6b4a" autoPlay muted loop playsInline aria-label="Demonstration of installing Resend from the Vercel Marketplace" />

### Vercel Dashboard

To install Resend from the Vercel Marketplace:

1. Log in to Vercel and go to the [Marketplace](https://vercel.com/resend/~/integrations/marketplace).
2. Search for "Resend" and click on the integration card.
3. Click on the "Install" button.
4. To create a new Resend account for your Vercel project, click on the "Create Account" option and **Continue**.
5. Click **Accept and Create** to continue the installation.
6. Choose a domain in the selector. Use a domain already on your Vercel account, or purchase one from Vercel.
7. Select the region your emails will be sent from (defaults to North Virginia).
8. Select a plan (free or paid).
9. Click **Continue** and **Create** to complete the installation.
10. Select your Vercel project to connect the domain to Resend and click **Connect**.

Vercel creates a new Resend account for your Vercel project, connects the domain to Resend, and provisions an API key.

### Vercel CLI

Add Resend to the linked project from your terminal. With the [Vercel CLI](https://vercel.com/docs/cli) installed:

1. Run `vc i resend` from your project directory. To set the region your emails will be sent from, pass it as metadata: `-m region=eu-west-1` (defaults to `us-east-1`). Supported regions: `us-east-1`, `eu-west-1`, `sa-east-1`, and `ap-northeast-1`.
2. Choose a domain in the selector. Use a domain already on your Vercel account, or purchase one from Vercel.
3. Select the region your emails will be sent from (defaults to North Virginia).
4. Select a plan (free or paid).
5. Click **Continue** and **Create** to complete the installation.
6. Select your Vercel project to connect the domain to Resend and click **Connect**.
7. Click **Complete onboarding** to view the domain in your new Resend account.
8. Click **Auto configure** to automatically add the DNS records to your Vercel domain.

Get more help adding a custom domain in [Resend's documentation](https://resend.com/docs/dashboard/domains/introduction.md).

### v0

[v0](https://v0.dev) by Vercel is a platform for building web sites, tools, apps, and projects via chat. Ask v0 to add email with Resend, then click **Install** when the chat prompts you. That opens the same Marketplace install flow as the [Vercel Dashboard](#vercel-dashboard) and [Vercel CLI](#vercel-cli).

The integration creates a Resend account, adds a Resend API key to your v0 project's environment variables, and configures DNS for a domain purchased in Vercel. Billing is managed through v0.

See [Send emails with v0 and Resend](https://resend.com/docs/v0-integration.md) for the full walkthrough.

## Billing

Vercel bills accounts created through the Marketplace. For Dashboard and CLI installations, choose and change your plan from the [billing settings](https://vercel.com/docs/integrations/create-integration/billing) of the Resend installation in Vercel. For v0 installations, v0 manages billing.

* **Free plan:** each user can have one free Resend team. If your email already belongs to a Resend team, you can only choose a paid plan.
* **Pay-as-you-go:** on a paid transactional plan, you can turn on email [overages](https://resend.com/docs/knowledge-base/account-quotas-and-limits.md#overage-limits), [Automations](https://resend.com/docs/knowledge-base/what-is-resend-pricing.md#automations), and extra [Inboxes](https://resend.com/docs/knowledge-base/account-quotas-and-limits.md#inbox-limits) from the Resend dashboard. Vercel bills these charges with your plan.
* **Refunds:** to request a refund, [contact Resend support](https://resend.com/help).

> [!WARNING]
>
> Discounts, promo codes, and startup or partner credits do not apply to Vercel
> Marketplace accounts. Some features are unavailable for Vercel Marketplace
> accounts, including some add-ons (e.g., dedicated IPs) and Resend Marketing
> plans.

## Manage the integration

### Uninstall

To uninstall, open the Resend integration in Vercel, go to **Settings**, and click **Delete Resend**.

> [!WARNING]
>
> Uninstalling Resend in Vercel permanently deletes your Resend team, including
> its domains and API keys. This can't be undone.

While the integration is installed, the team, its Vercel-managed domain, and your Resend account can't be deleted from the Resend dashboard.

### Move to another Vercel team

You can move the integration, and the Resend team it manages, to a different Vercel team. Your API keys, domains, and plan stay the same.

Before you start:

* The destination Vercel team must not have Resend installed.
* For a paid plan, the destination team needs a payment method in Vercel.
* The source team can't have an unpaid invoice for the integration.

> [!WARNING]
>
> Don't deploy until you've finished all 4 steps, including automatic
> deployments such as pushes to a connected Git branch, merged pull requests,
> and teammates' pushes. Don't uninstall Resend from the source Vercel team
> either. That installation owns your Resend team, and uninstalling it deletes
> the team with all its domains and API keys.

1. In the source Vercel team, open the Resend integration, click your installed product, and copy its `RESEND_API_KEY` somewhere safe as a backup.
2. Under **Projects**, click ⋮ on each project and choose **Remove Project Connection**. Don't delete the installed product.
3. Go to the installation **Settings**, click **Transfer Integration**, choose the destination team, and confirm.
4. In the destination team, open the installed product, go to **Projects**, and click **Connect to Project** for each project.

After the move, the main contact of the destination Vercel team becomes the Resend team's admin. Other members can sign in with **Open in Resend** from Vercel.

See Vercel's guide to [transferring an integration](https://vercel.com/docs/integrations/install-an-integration/transferring-an-integration) for more detail.

## Next steps

* Send your first email with [Next.js](https://resend.com/docs/send-with-nextjs.md).
* Explore [receiving emails](https://resend.com/docs/dashboard/receiving/introduction.md) with Resend.
* Use Resend [Templates](https://resend.com/docs/dashboard/templates/introduction.md) to simplify your email sending and design.
* Create your first Resend [Automation](https://resend.com/docs/dashboard/automations/introduction.md).
