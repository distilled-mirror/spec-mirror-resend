> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Elixir

> Learn how to send your first email using the Resend Elixir SDK.

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
          {:resend, "~> 0.4.0"}
        ]
      end
      ```
    </CodeGroup>
  </Step>

  <Step title="Send email using HTML">
    The easiest way to send an email is by using the `html` parameter.

    ```elixir send.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
    client = Resend.client(api_key: System.get_env("RESEND_API_KEY"))

    Resend.Emails.send(client, %{
      from: "Acme <onboarding@resend.dev>",
      to: ["delivered@resend.dev"],
      subject: "hello world",
      html: "<strong>it works!</strong>"
    })
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
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

  <Card title="Phoenix App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/phoenix_app">
    Full Phoenix web framework application
  </Card>
</CardGroup>
