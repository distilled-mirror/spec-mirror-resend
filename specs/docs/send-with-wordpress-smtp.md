> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using WordPress with SMTP

> Learn how to send your first email using Wordpress.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key.md)
* A [verified domain](/docs/add-a-domain.md)

## Guide

**1. Install a plugin**

First, you'll need to install and activate the [WP Mail SMTP](https://wordpress.org/plugins/wp-mail-smtp/) plugin. Once the plugin is activated you will see the setup wizard. You can skip this step as we'll guide you through how to configure the plugin for Resend. Click on **Go to the Dashboard** at the bottom of the screen to exit the setup wizard.

![WP Mail SMTP - Setup Wizard](https://mintcdn.com/resend/lyl6PQTYhtWhUjuS/images/wordpress-setup-wizard.png?fit=max\&auto=format\&n=lyl6PQTYhtWhUjuS\&q=85\&s=034e82ed82a43c1cc25e9119995ac558)

**2. Configuration**

From your admin dashboard, visit the **WP Mail SMTP > Settings** page to configure the plugin. Firstly, configure your **From Email**, **From Name**, and **Return Path**. Next, we'll configure the SMTP settings for Resend. Select **Other SMTP** in the **Mailer** section.

![WP Mail SMTP - Settings](https://mintcdn.com/resend/lyl6PQTYhtWhUjuS/images/wordpress-configure.png?fit=max\&auto=format\&n=lyl6PQTYhtWhUjuS\&q=85\&s=12cb502dcffbc76cad7f6bbef00a7f43)

In the **Other SMTP** section, configure the following settings:

* **SMTP Host**: `smtp.resend.com`
* **Encryption**: `SSL`
* **SMTP Port**: `465`
* **Auto TLS**: `ON`
* **Authentication**: `ON`
* **SMTP Username**: `resend`
* **SMTP Password**: `YOUR_API_KEY`

Make sure to replace `YOUR_API_KEY` with an existing key or create a new [API Key](https://resend.com/api-keys).

**3. Sending a test email**

From your admin dashboard, visit the **WP Mail SMTP > Tools** page to send a test email.

![WP Mail SMTP - Send a Test Email](https://mintcdn.com/resend/lyl6PQTYhtWhUjuS/images/wordpress-test-email.png?fit=max\&auto=format\&n=lyl6PQTYhtWhUjuS\&q=85\&s=bffb755f5673f14a03d84d36a4b361ca)
