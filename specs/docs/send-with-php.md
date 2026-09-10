> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with PHP

> Learn how to send your first email using the Resend PHP SDK.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

Prefer watching a video? Check out this video walkthrough below.

<YouTube id="vJRJ7b4QJHw" />

## Guide

<Steps>
  <Step title="Install">
    Get the Resend PHP SDK.

    ```bash Composer theme={"theme":{"light":"github-light","dark":"vesper"}}
    composer require resend/resend-php
    ```
  </Step>

  <Step title="Send email using HTML">
    The easiest way to send an email is by using the `html` parameter.

    ```php index.php theme={"theme":{"light":"github-light","dark":"vesper"}}
    <?php

    require __DIR__ . '/vendor/autoload.php';

    $resend = Resend::client('re_xxxxxxxxx');

    $resend->emails->send([
      'from' => 'Acme <onboarding@resend.dev>',
      'to' => ['delivered@resend.dev'],
      'subject' => 'hello world',
      'html' => '<strong>it works!</strong>',
    ]);
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
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

  <Card title="Symfony App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/symfony_app">
    Full Symfony web application
  </Card>
</CardGroup>
