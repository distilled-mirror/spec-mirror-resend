> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Laravel with SMTP

> Learn how to send your first email using Laravel with SMTP.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Setup your environment">
    First, configure your Resend SMTP details in your application's `.env` file:

    ```ini .env theme={"theme":{"light":"github-light","dark":"vesper"}}
    MAIL_MAILER=smtp
    MAIL_HOST=smtp.resend.com
    MAIL_PORT=587
    MAIL_USERNAME=resend
    MAIL_PASSWORD=re_xxxxxxxxx
    MAIL_ENCRYPTION=tls
    MAIL_FROM_ADDRESS=onboarding@resend.dev
    MAIL_FROM_NAME=Acme
    ```
  </Step>

  <Step title="Send an email">
    Now you're ready to send emails with Laravel's powerful email service. Here's an example of how to send your first email using Resend SMTP:

    ```php OrderShipmentController.php theme={"theme":{"light":"github-light","dark":"vesper"}}
    <?php

    namespace App\Http\Controllers;

    use App\Http\Controllers\Controller;
    use App\Mail\OrderShipped;
    use App\Models\Order;
    use Illuminate\Http\RedirectResponse;
    use Illuminate\Http\Request;
    use Illuminate\Support\Facades\Mail;

    class OrderShipmentController extends Controller
    {
        /**
         * Ship the given order.
         */
        public function store(Request $request): RedirectResponse
        {
            $order = Order::findOrFail($request->order_id);

            // Ship the order...

            Mail::to($request->user())->send(new OrderShipped($order));

            return redirect('/orders');
        }
    }
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Email Sending" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/laravel-resend-examples/app/Http/Controllers/EmailController.php">
    Basic, scheduled, attachments, CID, templates, and prevent threading
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/laravel-resend-examples/app/Http/Controllers/WebhookController.php">
    Handle webhook events
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/laravel-resend-examples/app/Http/Controllers/DoubleOptinController.php">
    Double opt-in subscription flow
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/laravel-resend-examples/app/Http/Controllers/AudienceController.php">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/laravel-resend-examples/app/Http/Controllers/DomainController.php">
    Create and manage sending domains
  </Card>
</CardGroup>
