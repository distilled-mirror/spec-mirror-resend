> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Resend CLI

> Learn how to send your first email using the Resend CLI.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key.md)
* A [verified domain](/docs/add-a-domain.md)

## Guide

**1. Install**

**cURL**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -fsSL https://resend.com/install.sh | bash
```

**npm**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
npm install -g resend-cli
```

**Homebrew**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
brew install resend/cli/resend
```

**PowerShell (Windows)**

```powershell theme={"theme":{"light":"github-light","dark":"vesper"}}
irm https://resend.com/install.ps1 | iex
```

**2. Authenticate**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend login
```

**3. Send email**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Hello World" \
  --text "Sent from my terminal."
```

## Next steps

> **[CLI Reference](/docs/cli.md)**
>
> Explore the full command reference, authentication options, and CI/CD
> examples.
