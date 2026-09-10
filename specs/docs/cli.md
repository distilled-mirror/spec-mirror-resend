> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Resend CLI

> The official command-line tool for Resend. Send emails, manage your account, and develop locally from the terminal.

The [Resend CLI](https://github.com/resend/resend-cli) is the official command-line interface for Resend. It covers the full API surface and is built for humans, AI agents, and CI/CD pipelines.

## Installation

<Tabs>
  <Tab title="cURL">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    curl -fsSL https://resend.com/install.sh | bash
    ```
  </Tab>

  <Tab title="npm">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli
    ```
  </Tab>

  <Tab title="Homebrew">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    brew install resend/cli/resend
    ```
  </Tab>

  <Tab title="PowerShell (Windows)">
    ```powershell theme={"theme":{"light":"github-light","dark":"vesper"}}
    irm https://resend.com/install.ps1 | iex
    ```
  </Tab>
</Tabs>

## Authentication

The CLI resolves your API key using the following priority chain:

| Priority    | Source                   | How to set                                |
| ----------- | ------------------------ | ----------------------------------------- |
| 1 (highest) | `--api-key` flag         | `resend --api-key re_xxx emails send ...` |
| 2           | `RESEND_API_KEY` env var | `export RESEND_API_KEY=re_xxx`            |
| 3 (lowest)  | Saved credentials        | `resend login`                            |

If no key is found from any source, the CLI errors with code `auth_error`.

**`resend login`**

Authenticate by storing your API key locally. The key is validated against the Resend API before being saved.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend login
```

In a terminal, the command prompts for your key via masked input. In non-interactive environments (CI, pipes), use the `--key` flag:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend login --key re_xxxxxxxxxxxxx
```

Credentials are saved to your system's secure credential storage (macOS Keychain, Windows Credential Manager, or Linux secret service).

| Flag          | Description                                         |
| ------------- | --------------------------------------------------- |
| `--key <key>` | API key to store (required in non-interactive mode) |

**`resend logout`**

Remove your saved API key.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend logout
```

**Switch between profiles**

If you work across multiple Resend teams or accounts, switch between profiles without logging in and out:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend auth switch
```

Use the global `--profile` flag on any command to run it with a specific profile:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend domains list --profile production
```

Other profile management commands:

| Command                          | Description                        |
| -------------------------------- | ---------------------------------- |
| `resend auth list`               | List all profiles                  |
| `resend auth switch [name]`      | Switch the active profile          |
| `resend auth rename [old] [new]` | Rename a profile                   |
| `resend auth remove [name]`      | Remove a profile                   |
| `resend whoami`                  | Show current authentication status |

## Emails

Send, retrieve, cancel, and manage email delivery.

**`resend emails send`**

Send an email. Provide all options via flags for scripting, or let the CLI prompt interactively for missing fields.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Hello World" \
  --text "It works!"
```

| Flag                        | Required         | Description                                                |
| --------------------------- | ---------------- | ---------------------------------------------------------- |
| `--from <address>`          | Yes \*           | Sender email address (must be from a verified domain)      |
| `--to <addresses...>`       | Yes              | One or more recipient email addresses (space-separated)    |
| `--subject <subject>`       | Yes \*           | Email subject line                                         |
| `--text <text>`             | One of text/html | Plain text body                                            |
| `--text-file <path>`        | One of text/html | Path to a plain text file (use `-` for stdin)              |
| `--html <html>`             | One of text/html | HTML body as a string                                      |
| `--html-file <path>`        | One of text/html | Path to an HTML file (use `-` for stdin)                   |
| `--react-email <path>`      | One of text/html | Path to a React Email template (`.tsx`) to render and send |
| `--cc <addresses...>`       | No               | CC recipients                                              |
| `--bcc <addresses...>`      | No               | BCC recipients                                             |
| `--reply-to <address>`      | No               | Reply-to email address                                     |
| `--scheduled-at <datetime>` | No               | Schedule for later (ISO 8601 or natural language)          |
| `--attachment <paths...>`   | No               | File path(s) to attach                                     |
| `--headers <key=value...>`  | No               | Custom headers as key=value pairs                          |
| `--tags <name=value...>`    | No               | Email tags as name=value pairs                             |
| `--idempotency-key <key>`   | No               | Deduplicate this send request                              |
| `--template <id>`           | No               | Template ID to use                                         |
| `--var <key=value...>`      | No               | Template variables as key=value pairs                      |

\* Not required when using `--template`, which provides them.

**Examples:**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
# HTML from a file
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Hello World" \
  --html-file ./welcome.html

# Multiple recipients with CC, BCC, and reply-to
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Hello World" \
  --text "It works!" \
  --cc manager@example.com \
  --bcc archive@example.com \
  --reply-to noreply@example.com

# Send a React Email template
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Hello World" \
  --react-email ./emails/welcome.tsx

# Send with a template
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --template tmpl_xxxxx \
  --var "name=Alice" --var "company=Acme"
```

**`resend emails batch`**

Send up to 100 emails in a single API request from a JSON file.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails batch --file ./emails.json
```

| Flag                        | Required | Description                                                                                |
| --------------------------- | -------- | ------------------------------------------------------------------------------------------ |
| `--file <path>`             | Yes      | Path to JSON file containing array of email objects (use `-` for stdin)                    |
| `--react-email <path>`      | No       | Path to a React Email template (`.tsx`). Rendered HTML applies to every email in the batch |
| `--idempotency-key <key>`   | No       | Deduplicate this batch request                                                             |
| `--batch-validation <mode>` | No       | `strict` (default, entire batch fails on any error) or `permissive`                        |

Each email in the JSON array supports the same fields as `resend emails send`, including per-email `scheduled_at` (natural language or ISO 8601) and `tags`. The `attachments` field is not supported in batch sends.

```json emails.json theme={"theme":{"light":"github-light","dark":"vesper"}}
[
  {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["foo@gmail.com"],
    "subject": "hello world",
    "html": "<h1>it works!</h1>",
    "scheduled_at": "in 1 min",
    "tags": [{ "name": "category", "value": "welcome" }]
  },
  {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["bar@outlook.com"],
    "subject": "world hello",
    "html": "<p>it works!</p>",
    "scheduled_at": "in 5 min"
  }
]
```

**Other email commands**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails list                # List sent emails
resend emails get <id>            # Retrieve a sent email by ID
resend emails cancel <id>         # Cancel a scheduled email
resend emails update <id>         # Update a scheduled email's send time
```

## Receiving

Process inbound emails, download attachments, and stream incoming messages.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails receiving list              # List received (inbound) emails
resend emails receiving get <id>          # Retrieve a received email with full details
resend emails receiving listen            # Poll for new inbound emails as they arrive
resend emails receiving forward <id>      # Forward a received email
resend emails receiving attachments <id>  # List attachments for a received email
resend emails receiving attachment <id> <attachment-id>  # Download a specific attachment
```

## Domains

Manage your sending and receiving domains.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend domains create --name example.com --region us-east-1
resend domains list               # List all domains
resend domains get <id>           # Retrieve domain with DNS records
resend domains verify <id>        # Trigger DNS verification
resend domains update <id>        # Update TLS, tracking, or receiving settings
resend domains delete <id>        # Delete a domain
```

## API Keys

Create, list, and revoke API keys for programmatic access.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend api-keys create --name "Production" --permission full_access
resend api-keys list              # List all API keys
resend api-keys delete <id>       # Delete an API key
```

## Broadcasts

Create and send broadcast emails to segments.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend broadcasts create \
  --from "Acme <onboarding@resend.dev>" \
  --subject "Product update" \
  --segment-id seg_xxxxx \
  --html-file ./broadcast.html \
  --send
resend broadcasts list            # List all broadcasts
resend broadcasts get <id>        # Retrieve broadcast details
resend broadcasts send <id>       # Send a draft broadcast
resend broadcasts update <id>     # Update a draft broadcast
resend broadcasts delete <id>     # Delete a broadcast
resend broadcasts open [id]       # Open a broadcast in the dashboard
```

## Contacts

Manage contacts, segment membership, and topic subscriptions.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contacts create --email steve.wozniak@gmail.com --first-name Steve
resend contacts list              # List all contacts
resend contacts get <id>          # Retrieve a contact by ID or email
resend contacts update <id>       # Update contact properties
resend contacts delete <id>       # Delete a contact
resend contacts segments <id>     # List segments a contact belongs to
resend contacts add-segment <id>  # Add a contact to a segment
resend contacts remove-segment <id> <segment-id>  # Remove from a segment
resend contacts topics <id>       # List topic subscriptions
resend contacts update-topics <id>  # Update topic subscriptions
resend contacts imports create --file ./contacts.csv  # Import contacts from CSV
resend contacts imports get <id>   # Retrieve import status and counts
resend contacts imports list       # List past contact imports
```

**`resend contacts imports create`**

Start an asynchronous CSV import. The command uploads the file and returns a
contact import ID immediately. Use `resend contacts imports get <id>` to check
processing status.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contacts imports create \
  --file ./contacts.csv \
  --column-map '{"email":"Email","firstName":"First Name","lastName":"Last Name"}' \
  --on-conflict upsert
```

| Flag                   | Required | Description                                                                    |
| ---------------------- | -------- | ------------------------------------------------------------------------------ |
| `--file <path>`        | Yes      | Path to the CSV file to import. Maximum file size is 200MB                     |
| `--column-map <json>`  | No       | JSON object mapping CSV headers to contact fields                              |
| `--on-conflict <mode>` | No       | `upsert` to update existing contacts or `skip` to leave them unchanged         |
| `--segment-id <id...>` | No       | Segment IDs to add imported contacts to. Repeat the flag for multiple segments |
| `--topics <json>`      | No       | JSON array of topic subscriptions with `id` and `subscription` fields          |

Without `--column-map`, CSV headers must match the lowercase contact field
names exactly: `email`, `first_name`, and `last_name`. Use `--column-map` when
your CSV uses headers like `Email` or `First Name`.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
# Import contacts and add them to a segment
resend contacts imports create \
  --file ./contacts.csv \
  --segment-id 78261eea-8f8b-4381-83c6-79fa7120f1cf

# Map custom properties and topic subscriptions
resend contacts imports create \
  --file ./contacts.csv \
  --column-map '{"email":"Email","properties":{"plan":{"column":"Plan","type":"string"}}}' \
  --topics '[{"id":"b6d24b8e-af0b-4c3c-be0c-359bbd97381e","subscription":"opt_in"}]'
```

**`resend contacts imports get`**

Retrieve a contact import by ID, including status and row counts.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contacts imports get 479e3145-dd38-476b-932c-529ceb705947
```

**`resend contacts imports list`**

List contact imports. The default limit is `10`.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contacts imports list --status completed
```

| Flag                | Required | Description                                                        |
| ------------------- | -------- | ------------------------------------------------------------------ |
| `--limit <n>`       | No       | Maximum number of imports to return. Must be between `1` and `100` |
| `--after <cursor>`  | No       | Return imports after this contact import ID                        |
| `--before <cursor>` | No       | Return imports before this contact import ID                       |
| `--status <status>` | No       | Filter by `queued`, `in_progress`, `completed`, or `failed`        |

## Contact Properties

Define custom properties to store additional data on contacts.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contact-properties create --key "company" --type string
resend contact-properties list | get | update | delete
```

## Segments

Group contacts into targetable segments for broadcasts.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend segments create --name "VIPs"
resend segments list              # List all segments
resend segments get <id>          # Retrieve a segment by ID
resend segments contacts <id>     # List contacts in a segment
resend segments delete <id>       # Delete a segment
```

## Topics

Manage subscription topics that contacts can opt in or out of.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend topics create --name "Product updates"
resend topics list | get | update | delete
```

## Suppressions

Manage the suppression list.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend suppressions list                              # List suppressed addresses (alias: ls)
resend suppressions list --origin bounce              # Filter by origin: bounce | complaint | manual
resend suppressions add spam@example.com              # Suppress a single address
resend suppressions get spam@example.com              # Retrieve by ID or email
resend suppressions delete spam@example.com --yes     # Remove by ID or email (alias: rm)
resend suppressions batch add --file ./emails.json    # Suppress up to 100 from a JSON array of emails
resend suppressions batch remove --file ./emails.json # Remove up to 100 (add --ids to treat entries as IDs)
```

## Templates

Create and manage email templates.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend templates create --name "Welcome" --subject "Welcome to Acme" --react-email ./emails/welcome.tsx
resend templates list             # List all templates
resend templates get <id>         # Retrieve a template by ID or alias
resend templates update <id>      # Update a template
resend templates publish <id>     # Publish a draft template
resend templates duplicate <id>   # Duplicate a template
resend templates delete <id>      # Delete a template
resend templates open [id]        # Open a template in the dashboard
```

## Logs

View API request logs.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend logs list              # List API request logs
resend logs get <id>          # Retrieve a log with full request/response bodies
resend logs open [id]         # Open logs in the dashboard
```

## Webhooks

Register endpoints and listen for email event notifications.

**`resend webhooks create`**

Register a webhook endpoint.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend webhooks create \
  --endpoint https://example.com/webhook \
  --events email.sent email.delivered
```

| Flag                  | Required | Description                                            |
| --------------------- | -------- | ------------------------------------------------------ |
| `--endpoint <url>`    | Yes      | HTTPS URL to receive events                            |
| `--events <types...>` | Yes      | Event types to subscribe to (use `all` for all events) |

**`resend webhooks listen`**

Listen for webhook events locally during development. Starts a server, registers a temporary webhook, streams events, and cleans up on exit.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend webhooks listen \
  --url https://hostname.tailnet-name.ts.net \
  --events email.received
```

| Flag                  | Required | Description                                                       |
| --------------------- | -------- | ----------------------------------------------------------------- |
| `--url <url>`         | Yes      | Your public URL (e.g., Tailscale Funnel URL)                      |
| `--events <types...>` | No       | Event types to listen for (default: `all`)                        |
| `--forward-to <url>`  | No       | Forward payloads to a local server (passes original Svix headers) |
| `--port <port>`       | No       | Local server port (default: 4318)                                 |

<Info>
  See the [webhook events documentation](/docs/webhooks/event-types) for the full
  list of available event types. For agent-specific webhook patterns, see [CLI
  for AI Agents](/docs/cli-agents#closing-the-loop-with-webhooks).
</Info>

**Other webhook commands**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend webhooks list              # List all webhook endpoints
resend webhooks get <id>          # Retrieve a webhook configuration
resend webhooks update <id>       # Update endpoint URL, events, or status
resend webhooks delete <id>       # Delete a webhook endpoint
```

<Tip>
  Run `resend <command> --help` for the full list of flags and options on any command.
</Tip>

## Automations

Create, manage, and monitor event-driven automation workflows.

**`resend automations create`**

Create a new automation from a JSON file describing the workflow graph.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations create --file ./automation.json
```

| Flag                   | Required | Description                                                        |
| ---------------------- | -------- | ------------------------------------------------------------------ |
| `--name <name>`        | Yes \*   | Automation name                                                    |
| `--status <status>`    | No       | Initial status: `enabled` or `disabled` (default: `disabled`)      |
| `--steps <json>`       | Yes \*   | Steps array as JSON string                                         |
| `--connections <json>` | Yes \*   | Connections array as JSON string                                   |
| `--file <path>`        | Yes \*   | Path to JSON file with full automation payload (use `-` for stdin) |

\* Provide `--file`, or `--name` with `--steps` and `--connections`. When using `--file`, other flags override file values.

**Other automation commands**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations list              # List all automations
resend automations get <id>          # Retrieve an automation with steps and connections
resend automations update <id>       # Update an automation's status (enable or disable)
resend automations duplicate <id>    # Duplicate an automation
resend automations stop <id>         # Stop an enabled automation
resend automations delete <id>       # Delete an automation
resend automations open [id]         # Open an automation in the dashboard
```

**Automation runs**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations runs list <automation-id>                    # List runs for an automation
resend automations runs list <automation-id> --status running   # Filter by status
resend automations runs get --automation-id <id> --run-id <id>  # Retrieve a specific run
```

| Flag                | Required | Description                                                                       |
| ------------------- | -------- | --------------------------------------------------------------------------------- |
| `--status <status>` | No       | Filter by status: `running`, `completed`, `failed`, `cancelled` (comma-separated) |

## Events

Define and send events that trigger automations.

**`resend events send`**

Send an event to trigger matching automations for a contact.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend events send \
  --event user.created \
  --email steve.wozniak@gmail.com \
  --payload '{"plan":"pro"}'
```

| Flag                | Required       | Description                                            |
| ------------------- | -------------- | ------------------------------------------------------ |
| `--event <name>`    | Yes            | Event name (e.g. `user.created`)                       |
| `--contact-id <id>` | One of contact | Contact ID (mutually exclusive with `--email`)         |
| `--email <email>`   | One of contact | Contact email (mutually exclusive with `--contact-id`) |
| `--payload <json>`  | No             | Event payload as JSON string                           |

**Other event commands**

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend events create --name user.created --schema '{"plan":"string"}'
resend events list                   # List all event definitions
resend events get <id>               # Retrieve an event by ID or name
resend events update <id>            # Update an event's schema
resend events delete <id>            # Delete an event definition
resend events open                   # Open events in the dashboard
```

## Utility

Diagnose your setup, manage authentication, and configure shell completions.

**`resend doctor`**

Run environment diagnostics. Verifies your CLI version, API key, credential storage, and domain status.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend doctor
```

| Check                  | Pass                                  | Warn                                         | Fail            |
| ---------------------- | ------------------------------------- | -------------------------------------------- | --------------- |
| **CLI Version**        | Running latest                        | Update available                             | N/A             |
| **API Key**            | Key found (shows masked key + source) | N/A                                          | No key found    |
| **Credential Storage** | Secure backend (e.g., macOS Keychain) | Plaintext file fallback                      | N/A             |
| **API Validation**     | Verified domains exist                | Sending-only key, no domains, or all pending | API key invalid |

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
# JSON output
resend doctor --json
```

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "ok": true,
  "checks": [
    { "name": "CLI Version", "status": "pass", "message": "v1.7.0 (latest)" },
    {
      "name": "API Key",
      "status": "pass",
      "message": "re_...xxxx (source: env)"
    },
    {
      "name": "Credential Storage",
      "status": "pass",
      "message": "macOS Keychain"
    },
    { "name": "Domains", "status": "pass", "message": "2 verified, 0 pending" }
  ]
}
```

Exits `0` when all checks pass or warn. Exits `1` if any check fails.

**Other utility commands**

| Command                       | Description                                                     |
| ----------------------------- | --------------------------------------------------------------- |
| `resend whoami`               | Show current authentication status                              |
| `resend open`                 | Open the Resend dashboard in your browser                       |
| `resend update`               | Check for available CLI updates                                 |
| `resend completion [shell]`   | Generate shell completion scripts (bash, zsh, fish, powershell) |
| `resend completion --install` | Auto-install completions into your shell profile                |

## Global options

These flags work on every command:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend [global options] <command> [command options]
```

| Flag                   | Description                                            |
| ---------------------- | ------------------------------------------------------ |
| `--api-key <key>`      | Override API key for this invocation                   |
| `-p, --profile <name>` | Profile to use (overrides `RESEND_PROFILE` env var)    |
| `--json`               | Force JSON output even in interactive terminals        |
| `-q, --quiet`          | Suppress spinners and status output (implies `--json`) |
| `--insecure-storage`   | Save API key as plaintext instead of secure storage    |
| `--version`            | Print version and exit                                 |
| `--help`               | Show help text                                         |

## Output behavior

The CLI has two output modes that switch automatically:

| Mode            | When                   | Stdout         | Stderr            |
| --------------- | ---------------------- | -------------- | ----------------- |
| **Interactive** | Terminal (TTY)         | Formatted text | Spinners, prompts |
| **Machine**     | Piped, CI, or `--json` | JSON           | Nothing           |

Pipe to another command and JSON output activates:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
resend doctor | jq '.checks[].name'
resend emails send \
  --from "Acme <onboarding@resend.dev>" \
  --to delivered@resend.dev \
  --subject "Hello World" \
  --text "It works!" | jq '.id'
```

Errors always exit with code `1` and output structured JSON:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{ "error": { "message": "No API key found", "code": "auth_error" } }
```

## CI/CD

Set `RESEND_API_KEY` as an environment variable, with no `resend login` needed:

```yaml theme={"theme":{"light":"github-light","dark":"vesper"}}
# GitHub Actions
env:
  RESEND_API_KEY: ${{ secrets.RESEND_API_KEY }}
steps:
  - run: |
      resend emails send \
        --from "Acme <onboarding@resend.dev>" \
        --to delivered@resend.dev \
        --subject "Deploy complete" \
        --text "Version ${{ github.sha }} deployed."
```

## Configuration

| Item              | Path                  | Notes                                                               |
| ----------------- | --------------------- | ------------------------------------------------------------------- |
| Config directory  | `~/.config/resend/`   | Respects `$XDG_CONFIG_HOME` on Linux, `%APPDATA%` on Windows        |
| Credentials       | System secure storage | macOS Keychain, Windows Credential Manager, or Linux secret service |
| Install directory | `~/.resend/bin/`      | Respects `$RESEND_INSTALL`                                          |

<Card title="Using the CLI with AI Agents" icon="microchip-ai" href="/docs/cli-agents">
  Learn about Agent Skills, non-interactive mode, and local webhook development
  for AI agents.
</Card>
