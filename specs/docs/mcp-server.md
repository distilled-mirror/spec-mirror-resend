> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# MCP Server

> Connect your AI agent to Resend using the hosted MCP server.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

MCP is an open protocol that standardizes how applications provide context to LLMs. Among other benefits, it provides LLMs tools to act on your behalf. Resend offers both a [remote MCP server](#remote-mcp-server) and a [local MCP server](#local-mcp-server).

<YouTube id="GjLb4hFo2qg" />

## Remote MCP Server

Resend hosts the MCP server at:

```
https://mcp.resend.com/mcp
```

Connect any MCP client that supports remote servers (Streamable HTTP). There's nothing to install and no local process to run, which makes it the best option for web-based clients like Claude and hosted agent platforms.

When you connect, your client opens a browser window to log in to Resend and approve access using OAuth.

The [Resend plugin](https://github.com/resend/resend-skills) follows the [Agent Plugins](https://agent-plugins.org) spec. On clients that install that plugin, it adds this remote MCP server and the adjacent [Resend skills](/docs/resend-skill) together. `plugin.json` identifies the plugin, `skills/` holds the skills, and `mcp.json` points at `https://mcp.resend.com/mcp`.

Each tab below matches the install on that client's page at resend.com.

<Tabs>
  <Tab title="Claude">
    Connect Resend in one click from the [connector directory](https://claude.ai/directory/connectors/resend). The connector installs the MCP server and every Resend skill.

    To install only the MCP server, add it manually in Claude (web or desktop) from **Settings** > **Connectors** > **Add custom connector**:

    ```
    https://mcp.resend.com/mcp
    ```

    See the [Claude page](https://resend.com/claude).
  </Tab>

  <Tab title="Copilot">
    To use GitHub Copilot in VS Code, add the following to your `settings.json`:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcp": {
        "servers": {
          "resend": {
            "type": "http",
            "url": "https://mcp.resend.com/mcp"
          }
        }
      }
    }
    ```

    Install the skills separately:

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    npx skills add resend/resend-skills
    ```

    See the [GitHub Copilot page](https://resend.com/github-copilot).
  </Tab>

  <Tab title="Claude Code">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    claude plugin install resend@claude-plugins-official
    ```

    Then run `/mcp` in Claude Code and select **resend** to complete the OAuth login. The plugin installs the remote MCP server and every [Resend skill](/docs/resend-skill).

    See the [Claude Code page](https://resend.com/claude-code).
  </Tab>

  <Tab title="Cursor">
    Run `/add-plugin resend` in Cursor's chat to install the official plugin. It follows the Agent Plugins spec and installs the remote MCP server and every Resend skill.

    To connect only the MCP server, open the command palette and choose "Cursor Settings" > "MCP" > "Add new global MCP server".

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "url": "https://mcp.resend.com/mcp"
        }
      }
    }
    ```

    See the [Cursor page](https://resend.com/cursor).
  </Tab>

  <Tab title="Codex">
    Install the [Resend plugin](https://chatgpt.com/plugins/plugin_asdk_app_6a3c407853888191beddc2151c2b6f8b?open_in_codex) in one click. It follows the Agent Plugins spec and installs the remote MCP server and every Resend skill.

    To connect the MCP server on its own, use the Codex CLI:

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    codex mcp add resend --url https://mcp.resend.com/mcp
    ```

    See the [Codex page](https://resend.com/codex).
  </Tab>

  <Tab title="Hermes">
    Install the official Resend plugin. One command adds the remote MCP server and every Resend skill.

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    hermes plugins install resend/resend-skills --enable
    ```

    Store `RESEND_API_KEY` so Hermes can send on your behalf. You will be prompted on first use.

    See the [Hermes page](https://resend.com/hermes).
  </Tab>

  <Tab title="Grok Bot">
    In Grok Bot, install the Resend plugin. That adds every Resend skill.

    ```
    /install-plugin resend

    # Then add RESEND_API_KEY so Grok Bot can send on your behalf.
    ```

    See the [Grok Bot page](https://resend.com/grokbot).
  </Tab>

  <Tab title="OpenClaw">
    Add the remote MCP server, then sign in:

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    openclaw mcp add resend --url https://mcp.resend.com/mcp --transport streamable-http
    openclaw mcp login resend
    ```

    Ask OpenClaw to install the skills:

    ```
    Install the Resend skills: https://github.com/resend/resend-skills
    ```

    See the [OpenClaw page](https://resend.com/openclaw). For an inbox, see the [OpenClaw guide](/docs/openclaw-guide).
  </Tab>

  <Tab title="OpenCode">
    Add to your `opencode.json` config:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "$schema": "https://opencode.ai/config.json",
      "mcp": {
        "resend": {
          "type": "remote",
          "url": "https://mcp.resend.com/mcp",
          "enabled": true
        }
      }
    }
    ```
  </Tab>

  <Tab title="Antigravity">
    Add this to your `~/.gemini/config/mcp_config.json` file:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "serverUrl": "https://mcp.resend.com/mcp"
        }
      }
    }
    ```
  </Tab>

  <Tab title="Gemini CLI">
    Add this to your `~/.gemini/settings.json` file:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "httpUrl": "https://mcp.resend.com/mcp"
        }
      }
    }
    ```
  </Tab>

  <Tab title="Devin">
    In Devin, open **Settings** > **Connections** > **MCP Servers** and click **Add a custom MCP**. See the [Devin guide](/docs/guides/devin) for the full step-by-step.

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "transport": "HTTP",
          "url": "https://mcp.resend.com/mcp"
        }
      }
    }
    ```
  </Tab>

  <Tab title="Zed">
    Add this to your Zed `settings.json`:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "context_servers": {
        "resend": {
          "url": "https://mcp.resend.com/mcp"
        }
      }
    }
    ```
  </Tab>

  <Tab title="Warp">
    In Warp's Settings, navigate to **Agents** > **MCP servers**, and click **+ Add** to add a new server.

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "resend": {
        "serverUrl": "https://mcp.resend.com/mcp"
      }
    }
    ```
  </Tab>

  <Tab title="fx">
    [fx](https://fx.sh) is a tiny, open, native coding agent from Vercel Labs. Install it, then add Resend as an HTTP server:

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    curl -fsSL https://fx.sh/setup.sh | bash
    fx mcp add --transport http resend https://mcp.resend.com/mcp
    ```

    fx completes the OAuth login the first time it connects. Inside the fx shell, the equivalent is `/mcp add --transport http resend https://mcp.resend.com/mcp`.
  </Tab>
</Tabs>

***

*If your client runs somewhere a browser login isn't possible* (a server, CI, or a headless agent), pass a [Resend API key](https://resend.com/api-keys) as a Bearer token instead of using OAuth.

<Tabs>
  <Tab title="Claude Code">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    claude mcp add --transport http resend https://mcp.resend.com/mcp --header "Authorization: Bearer re_xxxxxxxxx"
    ```
  </Tab>

  <Tab title="JSON config">
    For clients configured with JSON (Cursor, Zed, and others), add an `Authorization` header:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "url": "https://mcp.resend.com/mcp",
          "headers": {
            "Authorization": "Bearer re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>
</Tabs>

## Local MCP Server

The hosted server runs the same open-source code that's available on NPM as [`resend-mcp`](https://github.com/resend/resend-mcp). If you prefer to run the server yourself, you can integrate it into any supported MCP client using `npx`. You'll need to:

* [Create an API key](/docs/create-an-api-key)
* [Verify your domain](/docs/add-a-domain)

The local server supports two transport modes: **stdio** (default) and **HTTP**.

Choose your preferred mode and client below to get started. Remember to replace `re_xxxxxxxxx` with your actual API key.

### Stdio Transport (Default)

<Tabs>
  <Tab title="Claude Desktop">
    Open Claude Desktop settings > "Developer" tab > "Edit Config".

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "command": "npx",
          "args": ["-y", "resend-mcp"],
          "env": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Copilot">
    To use GitHub Copilot in VS Code, add the following to your `settings.json`:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcp": {
        "servers": {
          "resend": {
            "command": "npx",
            "args": ["-y", "resend-mcp"],
            "env": {
              "RESEND_API_KEY": "re_xxxxxxxxx"
            }
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Claude Code">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    claude mcp add resend -e RESEND_API_KEY=re_xxxxxxxxx -- npx -y resend-mcp
    ```
  </Tab>

  <Tab title="Cursor">
    Open the command palette and choose "Cursor Settings" > "MCP" > "Add new global MCP server".

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "command": "npx",
          "args": ["-y", "resend-mcp"],
          "env": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Codex">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    codex mcp add resend \
      --env RESEND_API_KEY=re_xxxxxxxxx \
      -- npx -y resend-mcp
    ```
  </Tab>

  <Tab title="OpenCode">
    Add to your `opencode.json` config:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "$schema": "https://opencode.ai/config.json",
      "mcp": {
        "resend": {
          "type": "local",
          "command": ["npx", "-y", "resend-mcp"],
          "enabled": true,
          "environment": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Antigravity">
    Add this to your `~/.gemini/config/mcp_config.json` file:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "command": "npx",
          "args": ["-y", "resend-mcp"],
          "env": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Gemini CLI">
    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "command": "npx",
          "args": ["-y", "resend-mcp"],
          "env": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Devin">
    In Devin, open **Settings** > **Connections** > **MCP Servers** and click **Add a custom MCP**. See the [Devin guide](/docs/guides/devin) for the full step-by-step.

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
  </Tab>

  <Tab title="Zed">
    Add this to your Zed `settings.json`:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "context_servers": {
        "resend": {
          "command": "npx",
          "args": ["-y", "resend-mcp"],
          "env": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>

  <Tab title="Warp">
    In Warp's Settings, navigate to **Agents** > **MCP servers**, and click **+ Add** to add a new server.

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "resend": {
        "command": "npx",
        "args": ["-y", "resend-mcp"],
        "env": {
          "RESEND_API_KEY": "re_xxxxxxxxx"
        }
      }
    }
    ```
  </Tab>

  <Tab title="fx">
    Add this to your `~/.fx/mcp.json` file:

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcp": {
        "resend": {
          "type": "stdio",
          "command": ["npx", "-y", "resend-mcp"],
          "environment": {
            "RESEND_API_KEY": "re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>
</Tabs>

### HTTP Transport

Run the server over HTTP for remote or web-based integrations. In HTTP mode, each client authenticates by passing their Resend API key as a Bearer token in the `Authorization` header.

Start the server:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
npx -y resend-mcp --http --port 3000
```

The server will listen on `http://127.0.0.1:3000` and expose the MCP endpoint at `/mcp` using Streamable HTTP.

<Tabs>
  <Tab title="Claude Code">
    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    claude mcp add resend --transport http http://127.0.0.1:3000/mcp --header "Authorization: Bearer re_xxxxxxxxx"
    ```
  </Tab>

  <Tab title="Cursor">
    Open the command palette and choose "Cursor Settings" > "MCP" > "Add new global MCP server".

    ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
    {
      "mcpServers": {
        "resend": {
          "url": "http://127.0.0.1:3000/mcp",
          "headers": {
            "Authorization": "Bearer re_xxxxxxxxx"
          }
        }
      }
    }
    ```
  </Tab>
</Tabs>

You can also set the port via the `MCP_PORT` environment variable:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
MCP_PORT=3000 npx -y resend-mcp --http
```

### Options

You can pass additional arguments to configure the local server:

* `--key`: Your Resend API key (stdio mode only, since HTTP mode uses the Bearer token from the client)
* `--sender`: Default sender email address from a verified domain
* `--reply-to`: Default reply-to email address (can be specified multiple times)
* `--http`: Use HTTP transport instead of stdio (default: stdio)
* `--port`: HTTP port when using `--http` (default: 3000, or `MCP_PORT` env var)

**Environment variables:**

* `RESEND_API_KEY`: Your Resend API key (required for stdio, optional for HTTP since clients pass it via Bearer token)
* `SENDER_EMAIL_ADDRESS`: Default sender email address from a verified domain (optional)
* `REPLY_TO_EMAIL_ADDRESSES`: Comma-separated reply-to email addresses (optional)
* `MCP_PORT`: HTTP port when using `--http` (optional)

<Info>
  If you don't provide a sender email address, the MCP server will ask you to
  provide one each time you call the tool.
</Info>

## MCP Server tools

Resend's MCP server gives your AI agent native access to the full Resend platform through a single integration. You can manage all aspects of your email infrastructure using natural language.

* **Emails**: Send, list, get, cancel, update, and batch send emails. Supports HTML, plain text, attachments (local file, URL, or base64), CC/BCC, reply-to, scheduling, tags, and topic-based sending.
* **Received Emails**: List and read inbound emails. List and download received email attachments.
* **Inboxes** (beta): Create, list, get, update, and remove inboxes. Manage their threads, thread emails (get, reply, forward), labels, and drafts (create, update, send). Inboxes is in beta and is only available on the [remote MCP server](#remote-mcp-server), not the local `resend-mcp` package. [Reach out to us](https://resend.com/contact) to get access.
* **Templates**: Create, list, get, update, publish, duplicate, and remove email templates. Supports composing template content and `{{{VARIABLE}}}` placeholders.
* **Contacts**: Create, list, get, update, and remove contacts. Manage segment memberships, topic subscriptions, and CSV contact imports. Supports custom contact properties.
* **Broadcasts**: Create, send, list, get, update, and remove broadcast campaigns. Supports scheduling, personalization placeholders, and preview text.
* **Automations**: Create, list, get, update, duplicate, and remove automations. Review the runs of an automation.
* **Events**: Send events to trigger automations for a contact. Create, update, and remove event definitions.
* **Domains**: Create, list, get, update, remove, and verify sender domains. Configure tracking, TLS, and sending/receiving capabilities. Create and verify domain claims.
* **Segments**: Create, list, get, and remove audience segments.
* **Topics**: Create, list, get, update, and remove subscription topics.
* **Contact Properties**: Create, list, get, update, and remove custom contact attributes.
* **API Keys**: Create, list, and remove API keys.
* **Webhooks**: Create, list, get, update, and remove webhooks for event notifications.
* **Logs**: List and inspect API request logs, including full request and response bodies.
* **Editor**: Connect to (and disconnect from) the visual editor in the Resend dashboard, and read a draft's content while collaborating on broadcasts and templates.

Here are some real examples of what your agent can do with these tools:

* Turn a [Paper design](/docs/guides/paper) into a ready-to-send [Template](/docs/dashboard/templates/introduction) or [Broadcast](/docs/dashboard/broadcasts/introduction)
* [Bulk import contacts from a CSV](/docs/dashboard/audiences/contacts#bulk-upload-by-csv), upserting or skipping duplicates, and organize them into [Segments](/docs/dashboard/segments/introduction)
* Build [Automations](/docs/dashboard/automations/introduction) that send emails when a contact is created, updated, or triggers a [custom event](/docs/dashboard/automations/custom-events)
* Read and triage [inbound email](/docs/dashboard/receiving/introduction), download attachments, and send replies
* Schedule, reschedule, and cancel [scheduled emails](/docs/dashboard/emails/schedule-email)
* Debug failed API requests by inspecting the [request logs](/docs/dashboard/logs/introduction)
