> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Devin and Resend

> Learn how to install the Resend MCP server in Devin.ai so your agent can send emails, manage contacts, and run broadcasts.

[Devin](https://devin.ai) is an autonomous AI software engineer that can connect to external services through MCP (Model Context Protocol) servers. Adding Resend's MCP server gives Devin native access to send emails, manage contacts and broadcasts, verify domains, and more.

For the full list of capabilities, see the [MCP Server overview](https://resend.com/docs/mcp-server.md).

## Prerequisites

Before you start, make sure you have:

* A Devin account with access to the Settings menu
* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

## Guide

**1. Open Devin Settings**

In Devin, open the **Settings** menu from your account dropdown.

**2. Go to Connections > MCP Servers**

In the Settings sidebar, click **Connections**, then select the **MCP Servers** tab. Click **Add a custom MCP**.

![Selecting MCP Servers under Connections in Devin](https://mintcdn.com/resend/YZqtGqf82akku4IQ/images/devin-connections-mcp.png?fit=max\&auto=format\&n=YZqtGqf82akku4IQ\&q=85\&s=1e0d35803e6121917d042a84f9459cd0)

**3. Add the Resend MCP configuration**

Click **Import JSON** and paste the following configuration into the modal.

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "mcpServers": {
    "resend": {
      "command": "npx",
      "args": ["-y", "resend-mcp"],
      "env": {
        "RESEND_API_KEY": "re_xxxxxxxxx",
        "SENDER_EMAIL_ADDRESS": "onboarding@resend.dev"
      }
    }
  }
}
```

![Pasting the Resend MCP configuration in Devin](https://mintcdn.com/resend/YZqtGqf82akku4IQ/images/devin-mcp-config.png?fit=max\&auto=format\&n=YZqtGqf82akku4IQ\&q=85\&s=37b3b24c60d34f932db1dc7d7cdae104)

**4. Update the Environment Variables**

Scroll down and update the environment variables:

* `RESEND_API_KEY`: delete this and add it as a secret (see the next step).
* `SENDER_EMAIL_ADDRESS`: update this with your sender email address you've verified in the [Resend Dashboard](https://resend.com/domains).

  ![Update the environment variables](https://mintcdn.com/resend/YZqtGqf82akku4IQ/images/devin-update-env.png?fit=max\&auto=format\&n=YZqtGqf82akku4IQ\&q=85\&s=2e99d816ea35a7c58846fc0f0ea3cf87)

**5. Add the Resend API key as a secret**

Add the `RESEND_API_KEY` as a secret. Click **Save secret** to confirm.

![Adding the Resend API key as a Devin secret](https://mintcdn.com/resend/YZqtGqf82akku4IQ/images/devin-add-secret.png?fit=max\&auto=format\&n=YZqtGqf82akku4IQ\&q=85\&s=d10ab3297311c5cc67b2bf18d91c3409)

> [!NOTE]
>
> You can create a new API key in the [Resend
> Dashboard](https://resend.com/api-keys).

**6. Confirm and enable the MCP server**

Add a description, click **Install and Enable**, and confirm in the dialog. Devin will install the server and mark it as connected.

![Confirming the Resend MCP server in Devin](https://mintcdn.com/resend/YZqtGqf82akku4IQ/images/devin-confirm-mcp.png?fit=max\&auto=format\&n=YZqtGqf82akku4IQ\&q=85\&s=3cb215a070a170cdda1d967c5d7b10e1)

**7. Test the connection**

Ask Devin to send a test email. For example:

```text theme={"theme":{"light":"github-light","dark":"vesper"}}
Send a test email to delivered@resend.dev using the Resend MCP server. Subject: "Hello from Devin".
```

Devin will call the Resend MCP server and confirm the send.
