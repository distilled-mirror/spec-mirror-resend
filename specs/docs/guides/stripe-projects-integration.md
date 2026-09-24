> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Stripe Projects Integration

> Provision Resend for a project directly from Stripe and start sending email.

Resend is a provider on [Stripe Projects](https://projects.dev). One command gives your project a Resend account and an API key, ready to send. No signup form, and your agent can run it for you.

## What you get

* A Resend account created and linked to your Stripe account.
* One API key per project, managed by Stripe and synced to your environment.
* Full access to the Resend dashboard and API.
* Paid plans for newly provisioned accounts are billed to your Stripe account, alongside your other Stripe Projects services.

One Stripe account maps to one Resend team. Each project gets its own API key, and all projects share the team's sending quota.

## Add Resend to a project

You need the [Stripe CLI](https://docs.stripe.com/stripe-cli) with the `projects` plugin installed, and a project to install Resend to:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
stripe plugin install projects
stripe projects init
```

Then, run:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
stripe projects add resend/email
```

<Tip>
  You can also ask your coding agent to run these steps. `stripe projects init`
  writes Stripe Projects skills into the project, and `add resend/email` adds a
  Resend skill, so the agent knows the CLI commands and the Resend API.
</Tip>

The CLI asks you to pick a plan (Free or Pro), provisions the account, and writes the API key to your local `.env` as `RESEND_API_KEY`. Run `stripe projects env` to list the variables with their values hidden.

### Which email Resend uses

Resend uses the email on your Stripe account, not the email you sign in to Stripe with. On a company account the two often differ. If you sign in as `bob@example.com` and the Stripe account's email is `company@example.com`, Resend provisions for `company@example.com`. That address owns the Resend account, and it is the only recipient your test emails can go to.

### Create or link

What happens next depends on whether that email already has a Resend account:

* No Resend account yet: the CLI creates one on the plan you picked.
* An existing Resend account: the CLI links a team where that email is an admin, and asks which team when there are several. The team's plan carries over, and its billing stays at Resend.

You can use your key to access all features from the [Resend API](https://resend.com/docs/api-reference).

To open the Resend Dashboard, already signed in, run:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
stripe projects open resend
```

To rotate the key, run `stripe projects rotate resend/email`. The CLI writes the new key to your `.env` and the old one stops working.

## Send your first email

You can send before you verify a domain. Use `onboarding@resend.dev` as the `from` address. The recipient must be the email on your Stripe account, the one Resend provisioned for. That is the only recipient the `resend.dev` testing domain can deliver to.

Install the SDK and read the key from the environment. Replace `you@example.com` with that address.

The SDKs read the process environment, not the `.env` file. Load it first, for example with `node --env-file=.env send.mjs`, or with your language's dotenv package.

<CodeGroup>
  ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  npm install resend
  ```

  ```bash PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  composer require resend/resend-php
  ```

  ```bash Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  pip install resend
  ```

  ```bash Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  gem install resend
  ```

  ```bash Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  go get github.com/resend/resend-go/v3
  ```

  ```bash Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  cargo add resend-rs
  cargo add tokio -F macros,rt-multi-thread
  ```

  ```bash Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  implementation 'com.resend:resend-java:+'
  ```

  ```bash .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  dotnet add package Resend
  ```

  ```elixir Elixir theme={"theme":{"light":"github-light","dark":"vesper"}}
  def deps do
    [
      {:resend, "~> 0.4.0"}
    ]
  end
  ```
</CodeGroup>

Then send an email:

<CodeGroup>
  ```js Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend(process.env.RESEND_API_KEY);

  const { data, error } = await resend.emails.send({
    from: 'onboarding@resend.dev',
    to: ['you@example.com'],
    subject: 'Hello from Stripe Projects',
    html: '<strong>It works!</strong>',
  });

  if (error) {
    console.error(error);
  } else {
    console.log('Email sent:', data);
  }
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  <?php

  require __DIR__ . '/vendor/autoload.php';

  $resend = Resend::client(getenv('RESEND_API_KEY'));

  try {
      $result = $resend->emails->send([
          'from' => 'onboarding@resend.dev',
          'to' => ['you@example.com'],
          'subject' => 'Hello from Stripe Projects',
          'html' => '<strong>It works!</strong>',
      ]);
      echo 'Email sent: ' . $result['id'];
  } catch (Exception $e) {
      echo 'Error: ' . $e->getMessage();
  }
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import os
  import resend
  from resend.exceptions import ResendError

  resend.api_key = os.environ["RESEND_API_KEY"]

  params: resend.Emails.SendParams = {
      "from": "onboarding@resend.dev",
      "to": ["you@example.com"],
      "subject": "Hello from Stripe Projects",
      "html": "<strong>It works!</strong>",
  }

  try:
      email = resend.Emails.send(params)
      print("Email sent:", email)
  except ResendError as error:
      print(error)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = ENV["RESEND_API_KEY"]

  params = {
    "from": "onboarding@resend.dev",
    "to": ["you@example.com"],
    "subject": "Hello from Stripe Projects",
    "html": "<strong>It works!</strong>"
  }

  sent = Resend::Emails.send(params)
  puts "Email sent: #{sent[:id]}"
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"fmt"
  	"os"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	client := resend.NewClient(os.Getenv("RESEND_API_KEY"))

  	params := &resend.SendEmailRequest{
  		From:    "onboarding@resend.dev",
  		To:      []string{"you@example.com"},
  		Subject: "Hello from Stripe Projects",
  		Html:    "<strong>It works!</strong>",
  	}

  	sent, err := client.Emails.Send(params)
  	if err != nil {
  		fmt.Println(err.Error())
  		return
  	}
  	fmt.Println("Email sent:", sent.Id)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::CreateEmailBaseOptions;
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
      let api_key = std::env::var("RESEND_API_KEY")
          .expect("RESEND_API_KEY not set");
      let resend = Resend::new(&api_key);

      let email = CreateEmailBaseOptions::new(
          "onboarding@resend.dev",
          ["you@example.com"],
          "Hello from Stripe Projects"
      ).with_html("<strong>It works!</strong>");

      match resend.emails.send(email).await {
          Ok(data) => println!("Email sent: {:?}", data),
          Err(e) => eprintln!("Error: {}", e),
      }

      Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend(System.getenv("RESEND_API_KEY"));

          CreateEmailOptions params = CreateEmailOptions.builder()
              .from("onboarding@resend.dev")
              .to("you@example.com")
              .subject("Hello from Stripe Projects")
              .html("<strong>It works!</strong>")
              .build();

          try {
              CreateEmailResponse data = resend.emails().send(params);
              System.out.println("Email sent: " + data.getId());
          } catch (ResendException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( Environment.GetEnvironmentVariable( "RESEND_API_KEY" )! );

  try
  {
      var resp = await resend.EmailSendAsync( new EmailMessage()
      {
          From = "onboarding@resend.dev",
          To = "you@example.com",
          Subject = "Hello from Stripe Projects",
          HtmlBody = "<strong>It works!</strong>",
      } );
      Console.WriteLine( "Email sent: {0}", resp.Content );
  }
  catch ( ResendException ex )
  {
      Console.WriteLine( "Error: {0}", ex.Message );
  }
  ```

  ```elixir Elixir theme={"theme":{"light":"github-light","dark":"vesper"}}
  client = Resend.client(api_key: System.get_env("RESEND_API_KEY"))

  {:ok, result} = Resend.Emails.send(client, %{
    from: "onboarding@resend.dev",
    to: ["you@example.com"],
    subject: "Hello from Stripe Projects",
    html: "<strong>It works!</strong>"
  })

  IO.inspect(result)
  ```
</CodeGroup>

See the full quickstart for [Node.js](/docs/send-with-nodejs), [PHP](/docs/send-with-php), [Python](/docs/send-with-python), [Ruby](/docs/send-with-ruby), [Go](/docs/send-with-go), [Rust](/docs/send-with-rust), [Java](/docs/send-with-java), [.NET](/docs/send-with-dotnet), or [Elixir](/docs/send-with-elixir).

## Add a domain

Resend sends emails using a domain you own. Before you can send or receive emails with Resend to addresses other than your own, you must have a verified domain associated with your account.

To send from your own domain, and to any recipient, [add and verify a domain](/docs/add-a-domain).

## Billing

Resend offers free and paid plans through Stripe Projects. Stripe manages the billing, so you pay for Resend the same way you pay for your other Projects services.

To upgrade, run:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
stripe projects upgrade resend/email
```

The CLI asks you to confirm the plan change, then shows the plans to pick from. In a script or from an agent, name the current plan and the target, and pass `--json`:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
stripe projects upgrade resend/free resend/pro --json
```

If Stripe has no payment method for you yet, the CLI stops and gives you a Checkout link to add one. The higher quota activates when the first payment confirms. To go back to the free plan, run `stripe projects downgrade resend/pro resend/free`. The paid quota stays until the billing period ends.

<Warning>
  The Stripe Projects integration does not have paid marketing plans yet, only
  Transactional Pro. Discounts, promo codes, and startup or partner credits do
  not apply to Stripe Projects plans.
</Warning>

## Next steps

* Send your first email with [Next.js](/docs/send-with-nextjs).
* Explore [receiving emails](/docs/dashboard/receiving/introduction) with Resend.
* Use Resend [Templates](/docs/dashboard/templates/introduction) to simplify your email sending and design.
* Create your first Resend [Automation](/docs/dashboard/automations/introduction).
