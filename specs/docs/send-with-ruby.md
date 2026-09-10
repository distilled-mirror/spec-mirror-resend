> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Ruby

> Learn how to send your first email using the Resend Ruby SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the Resend Ruby SDK.

    <CodeGroup>
      ```bash RubyGems theme={"theme":{"light":"github-light","dark":"vesper"}}
      gem install resend
      ```

      ```bash Gemfile theme={"theme":{"light":"github-light","dark":"vesper"}}
      gem 'resend'
      ```
    </CodeGroup>
  </Step>

  <Step title="Send email using HTML">
    The easiest way to send an email is by using the `html` parameter.

    ```rb index.rb theme={"theme":{"light":"github-light","dark":"vesper"}}
    require "resend"

    Resend.api_key = "re_xxxxxxxxx"

    params = {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["delivered@resend.dev"],
      "subject": "hello world",
      "html": "<strong>it works!</strong>"
    }

    sent = Resend::Emails.send(params)
    puts sent
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/basic_send.rb">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/with_attachments.rb">
    Send emails with file attachments
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/with_template.rb">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/scheduled_send.rb">
    Schedule emails for future delivery
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/audiences.rb">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/domains.rb">
    Create and manage sending domains
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/inbound.rb">
    Receive and process inbound emails
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/examples/double_optin">
    Double opt-in subscription flow
  </Card>

  <Card title="Sinatra App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/sinatra_app">
    Full Sinatra web application
  </Card>

  <Card title="Rails App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/rails_app">
    Full Rails web application
  </Card>
</CardGroup>
