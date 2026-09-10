> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Rails

> Learn how to send your first email using Rails and the Resend Ruby SDK.

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

  <Step title="Send email using Rails Action Mailer">
    This gem can be used as an Action Mailer delivery method.

    First, let's update or create your mailer initializer file with your Resend API Key.

    ```rb config/initializers/mailer.rb theme={"theme":{"light":"github-light","dark":"vesper"}}
    Resend.api_key = "re_xxxxxxxxx"
    ```

    Add these lines of code into your environment config file.

    ```rb config/environments/environment.rb theme={"theme":{"light":"github-light","dark":"vesper"}}
    config.action_mailer.delivery_method = :resend
    ```

    Then create a `UserMailer` class definition.

    ```rb app/mailers/user_mailer.rb theme={"theme":{"light":"github-light","dark":"vesper"}}
    class UserMailer < ApplicationMailer
      default from: 'Acme <onboarding@resend.dev>' # this domain must be verified with Resend
      def welcome_email
        @user = params[:user]
        @url = 'http://example.com/login'
        mail(to: ["delivered@resend.dev"], subject: 'hello world')
      end
    end
    ```

    And create your ERB email template.

    ```html app/views/user_mailer/welcome_email.html.erb theme={"theme":{"light":"github-light","dark":"vesper"}}
    <!doctype html>
    <html>
      <head>
        <meta content="text/html; charset=UTF-8" http-equiv="Content-Type" />
      </head>
      <body>
        <h1>Welcome to example.com, <%= @user.name %></h1>
        <p>You have successfully signed up to example.com,</p>
        <p>To log in to the site, just follow this link: <%= @url %>.</p>
        <p>Thanks for joining and have a great day!</p>
      </body>
    </html>
    ```

    Initialize your `UserMailer` class. This returns an `ActionMailer::MessageDelivery` instance.

    ```rb theme={"theme":{"light":"github-light","dark":"vesper"}}
    u = User.new name: "derich"
    mailer = UserMailer.with(user: u).welcome_email

    # => #<ActionMailer::MessageDelivery:153700, @mail_message=#<Mail::Message...>, @processed_mailer=...>
    ```

    Finally, you can now send emails using the `deliver_now!` method:

    ```rb theme={"theme":{"light":"github-light","dark":"vesper"}}
    mailer.deliver_now!

    # => {:id=>"a193c81e-9ac5-4708-a569-5caf14220539", :from=>....}
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Rails App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/rails_app">
    Full Rails web application
  </Card>

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
</CardGroup>
