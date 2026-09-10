> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Symfony

> Learn how to send your first email using the Symfony Resend Mailer Bridge.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the Resend Mailer Bridge package.

    ```bash Composer theme={"theme":{"light":"github-light","dark":"vesper"}}
    composer require symfony/resend-mailer
    ```

    If your application relies on Resend webhook events, also install the Symfony Webhook Component.

    ```bash Composer theme={"theme":{"light":"github-light","dark":"vesper"}}
    composer require symfony/webhook
    ```
  </Step>

  <Step title="Configuring Mailer">
    In your `.env.local` file, which you can create if needed, add the following:

    ```sh theme={"theme":{"light":"github-light","dark":"vesper"}}
    MAILER_DSN=resend+api://API_KEY@default
    MAILER_RESEND_SECRET=SIGNING_SECRET
    ```

    Replace `API_KEY` with your Resend API key, and `SIGNING_SECRET` with your webhook secret, which can be retrieved from the Resend dashboard after creating a new webhook endpoint (see below).
  </Step>

  <Step title="Send your first email">
    In a controller, inject the `Mailer`:

    ```php theme={"theme":{"light":"github-light","dark":"vesper"}}
    public function __construct(
        private readonly MailerInterface $mailer,
    ) {
    }
    ```

    In a controller action, use the `$this->mailer` to send your email:

    ```php theme={"theme":{"light":"github-light","dark":"vesper"}}
    $this->mailer->send(
        (new Email())
            ->from('Acme <onboarding@resend.dev>')
            ->to('delivered@resend.dev')
            ->subject('Hello world')
            ->html('<strong>it works!</strong>')
    );
    ```

    Learn more about sending emails with Mailer Component in [Symfony's documentation](https://symfony.com/doc/current/mailer.html#creating-sending-messages).
  </Step>

  <Step title="Receive and handle webhooks">
    Thanks to the Webhook Component, you can create a webhook listener.

    ```php src/Webhook/ResendWebhookListener.php theme={"theme":{"light":"github-light","dark":"vesper"}}
    #[AsRemoteEventConsumer('mailer_resend')]
    readonly class ResendWebhookListener implements ConsumerInterface
    {
        public function __construct(
            #[Autowire(param: 'kernel.project_dir')] private string $projectDir,
        ) {
        }

        public function consume(RemoteEvent $event): void
        {
            if ($event instanceof MailerDeliveryEvent) {
                $this->handleMailDelivery($event);
            } elseif ($event instanceof MailerEngagementEvent) {
                $this->handleMailEngagement($event);
            } else {
                // This is not an email event
                return;
            }
        }

        private function handleMailDelivery(MailerDeliveryEvent $event): void
        {
            // Todo
        }

        private function handleMailEngagement(MailerEngagementEvent $event): void
        {
            // Todo
        }
    }
    ```

    Bind your listener to the Webhook routing config:

    ```yaml config/packages/webhook.yaml theme={"theme":{"light":"github-light","dark":"vesper"}}
    framework:
      webhook:
        routing:
          mailer_resend:
            service: 'mailer.webhook.request_parser.resend'
            secret: '%env(MAILER_RESEND_SECRET)%'
    ```

    Next, register your application's webhook endpoint URL (example: `https://{app_domain}/webhook/mailer_resend`) in the [Resend Dashboard](https://resend.com/webhooks):
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Symfony App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/symfony_app">
    Full Symfony web application
  </Card>

  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/send">
    Basic, batch, and prevent-threading send
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/attachments">
    File attachments and inline images (CID)
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/scheduling">
    Schedule emails for future delivery
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/templates">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/double-optin">
    Double opt-in subscription flow
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/inbound">
    Receive and process inbound emails
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/audiences">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/domains">
    Create and manage sending domains
  </Card>
</CardGroup>
