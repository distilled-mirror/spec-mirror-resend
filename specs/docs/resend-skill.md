> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Resend Skill

> Send emails through the Resend API with AI agents.

The Resend skill enables AI agents to send emails through the Resend API using our official recommendations. It provides a streamlined interface for sending single and batch emails with built-in error handling and retry logic.

## Installation

This skill is part of the [resend-skills](https://github.com/resend/resend-skills) repository, which also includes the [Agent Email Inbox skill](/docs/agent-email-inbox-skill) for secure inbound email processing. When you run the install command, you'll be prompted to choose which skills to install.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
npx skills add resend/resend-skills
```

Clients that support the [Agent Plugins](https://agent-plugins.org) spec can install the same repository as a plugin. That install adds these skills and the [remote MCP server](/docs/mcp-server) together. The [MCP server docs](/docs/mcp-server#remote-mcp-server) list the install command for each supported client.

## Advantages

Build with our official recommendations for sending emails with Resend.

* **Single and batch email sending**: Send individual emails or batch up to 100 emails per request.
* **Built-in error handling and retry logic**: Automatic retries with exponential backoff for transient failures.
* **Idempotency key support**: Prevent duplicate sends with idempotency keys for safe retries.
* **Multi-language SDK support**: Works with Node.js, Python, Ruby, Go, and other supported SDKs.
* **Automatic activation for email tasks**: AI agents automatically use this skill when email sending is needed.

## Learn More

<CardGroup cols={2}>
  <Card title="Agent Email Inbox" icon="inbox" href="/docs/agent-email-inbox-skill">
    Give your agent a secure inbox to receive and act on inbound emails.
  </Card>

  <Card title="View on GitHub" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-skills">
    See the full source code and documentation.
  </Card>
</CardGroup>
