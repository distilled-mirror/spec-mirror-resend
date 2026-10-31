> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Sinatra

> Learn how to send your first email using Sinatra and the Resend Ruby SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

## Guide

**1. Install**

Get the Resend Ruby SDK.

```bash RubyGems theme={"theme":{"light":"github-light","dark":"vesper"}}
gem install resend
```

```bash Gemfile theme={"theme":{"light":"github-light","dark":"vesper"}}
gem 'resend'
```

**2. Send email using HTML**

The easiest way to send an email is by using the `html` parameter.

```rb index.rb theme={"theme":{"light":"github-light","dark":"vesper"}}
require "sinatra"
require "resend"

set :port, 5000
set :bind, "0.0.0.0"

Resend.api_key = ENV["RESEND_API_KEY"]

get "/" do

  content_type :json

  params = {
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'hello world',
    html: '<strong>it works!</strong>',
  }

  Resend::Emails.send(params).to_hash.to_json
end
```

## Examples

> [card] [Sinatra App](https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/sinatra_app)
>
> Full Sinatra web application

> [card] [Basic Send](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/basic_send.rb)
>
> Basic email sending

> [card] [Attachments](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/with_attachments.rb)
>
> Send emails with file attachments

> [card] [Templates](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/with_template.rb)
>
> Send emails using Resend hosted templates

> [card] [Scheduling](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/scheduled_send.rb)
>
> Schedule emails for future delivery

> [card] [Audiences](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/audiences.rb)
>
> Manage contacts and audiences

> [card] [Domains](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/domains.rb)
>
> Create and manage sending domains

> [card] [Inbound Webhooks](https://github.com/resend/resend-examples/blob/main/ruby-resend-examples/examples/inbound.rb)
>
> Receive and process inbound emails

> [card] [Double Opt-in](https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/examples/double_optin)
>
> Double opt-in subscription flow
