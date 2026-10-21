> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with PHP

> Learn how to send your first email using the Resend PHP SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

Prefer watching a video? Check out this video walkthrough below.

[YouTube video player](https://www.youtube.com/embed/vJRJ7b4QJHw)

## Guide

**1. Install**

Get the Resend PHP SDK.

```bash Composer theme={"theme":{"light":"github-light","dark":"vesper"}}
composer require resend/resend-php
```

**2. Send email using HTML**

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

## Examples

> **[Basic Send](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/send)**
>
> Basic, batch, and prevent-threading send

> **[Attachments](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/attachments)**
>
> File attachments and inline images (CID)

> **[Scheduling](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/scheduling)**
>
> Schedule emails for future delivery

> **[Templates](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/templates)**
>
> Send emails using Resend hosted templates

> **[Double Opt-in](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/double-optin)**
>
> Double opt-in subscription flow

> **[Inbound Webhooks](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/inbound)**
>
> Receive and process inbound emails

> **[Audiences](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/audiences)**
>
> Manage contacts and audiences

> **[Domains](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/domains)**
>
> Create and manage sending domains

> **[Symfony App](https://github.com/resend/resend-examples/tree/main/php-resend-examples/symfony_app)**
>
> Full Symfony web application
