> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Phoenix

> Learn how to send your first email using Phoenix and the Resend Elixir SDK.

<Info>
  This guides utilizes an [open source
  library](https://github.com/elixir-saas/resend-elixir) contributed by a
  community member. It's not developed, maintained, or supported by Resend
  directly.
</Info>

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Install by adding `resend` to your list of dependencies in `mix.exs`:

    <CodeGroup>
      ```elixir mix.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
      def deps do
        [
          {:resend, "~> 0.4.5"}
        ]
      end
      ```
    </CodeGroup>
  </Step>

  <Step title="Send email using Swoosh">
    This library includes a Swoosh adapter to make using Resend with a new Phoenix project straightforward. Configure your Mailer:

    ```elixir theme={"theme":{"light":"github-light","dark":"vesper"}}
    config :my_app, MyApp.Mailer,
      adapter: Resend.Swoosh.Adapter,
      api_key: System.fetch_env!("RESEND_API_KEY")
    ```

    If you're configuring your app for production, configure your adapter in `prod.exs`, and your API key from the environment in `runtime.exs`:

    <CodeGroup>
      ```elixir prod.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
      config :my_app, MyApp.Mailer, adapter: Resend.Swoosh.Adapter
      ```

      ```elixir runtime.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
      config :my_app, MyApp.Mailer, api_key: "re_xxxxxxxxx"
      ```
    </CodeGroup>
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Phoenix App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/phoenix_app">
    Full Phoenix web framework application
  </Card>

  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/basic_send.exs">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/with_attachments.exs">
    Send emails with file attachments
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/with_template.exs">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/scheduled_send.exs">
    Schedule emails for future delivery
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/audiences.exs">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/domains.exs">
    Create and manage sending domains
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/inbound.exs">
    Receive and process inbound emails
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/examples/double_optin">
    Double opt-in subscription flow
  </Card>
</CardGroup>
