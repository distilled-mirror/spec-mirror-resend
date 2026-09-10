> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Resend CLI for AI Agents

> How to use the Resend CLI in AI agent workflows.

The [Resend CLI](/docs/cli) works out of the box for AI agents and CI/CD pipelines. This page covers agent-specific behavior. See the [CLI reference](/docs/cli) for installation, commands, and full documentation.

## Agent Skills

The Resend CLI includes built-in Agent Skills that help AI agents understand how to use the CLI effectively.

Install the skill using the following command:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
npx skills add resend/resend-cli
```

## Non-interactive mode

When the CLI detects a non-TTY environment (piped output, CI runner, or the `--json` flag), it automatically switches to machine-readable mode:

* **Output:** JSON to stdout, no progress indicators
* **Exit codes:** `0` for success, `1` for errors
* **Errors:** Always include `message` and `code` fields

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{ "error": { "message": "No API key found", "code": "auth_error" } }
```

All required flags must be provided. Interactive prompts are disabled. Missing flags cause an error listing what's needed.

## Piping from stdin

Agents generate content on the fly. Pass `-` to read from stdin instead of writing temp files:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
echo "Your order has shipped." | resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Order update" \
  --text-file -
```

This works with `--html-file -` on send and `--file -` on [batch commands](/docs/cli#emails).

## Batch sending

Send up to 100 emails in a single request by piping a JSON array into `emails batch`:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
cat emails.json | resend emails batch --file -
```

## Safe retries

Add `--idempotency-key` to prevent duplicates when your agent retries a failed request:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Welcome" \
  --text "Hello!" \
  --idempotency-key "welcome-user-123"
```

This flag is available on both `emails send` and `emails batch`.

## Scheduling

The `--scheduled-at` flag accepts ISO 8601 timestamps and natural language:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Your trial ends soon" \
  --text "Your free trial expires in 3 days." \
  --scheduled-at "tomorrow at 9am ET"
```

Cancel or reschedule with `resend emails cancel <id>` and `resend emails update <id> --scheduled-at <datetime>`.

## Reading inbound emails

Agents can process incoming email as an input source. Stream inbound emails as NDJSON with `emails receiving listen`:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails receiving listen --json
```

Or fetch a specific email with full content and attachments:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails receiving get <email-id>
```

This requires a [verified domain](/docs/dashboard/domains/introduction) with receiving enabled.

## Closing the loop with webhooks

When an agent sends an email, it often needs to know what happened next: was it delivered, did it bounce, did the recipient reply? The `webhooks listen` command gives your agent a real-time feedback loop by streaming [webhook events](/docs/webhooks/event-types) directly to the terminal.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend webhooks listen \
  --url https://hostname.tailnet-name.ts.net \
  --events email.delivered email.bounced email.received
```

The CLI registers a temporary webhook, streams matching events as JSON to stdout, and deletes the webhook when you exit (`Ctrl+C`). Use `--forward-to` to pipe payloads to a local server for processing:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend webhooks listen \
  --url https://hostname.tailnet-name.ts.net \
  --forward-to http://localhost:4321/api/webhook
```

The `--url` flag takes any public URL that points to the local server port (`4318` by default). Use any tunnel, such as [Tailscale Funnel](https://tailscale.com/kb/1223/funnel), [ngrok](https://ngrok.com/), or [localtunnel](https://theboringtech.io/).

<Tip>
  For a permanent setup, deploy a webhook handler and register it via `resend
      webhooks create` pointing to your production URL.
</Tip>
