> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using PHPMailer with SMTP

> Learn how to send your first email using PHPMailer with SMTP.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the [PHPMailer](https://github.com/PHPMailer/PHPMailer) package.

    <CodeGroup>
      ```bash php theme={"theme":{"light":"github-light","dark":"vesper"}}
      composer require phpmailer/phpmailer
      ```
    </CodeGroup>
  </Step>

  <Step title="Send email using SMTP">
    When configuring your SMTP integration, you'll need to use the following credentials:

    * **Host**: `smtp.resend.com`
    * **Port**: `587`
    * **Username**: `resend`
    * **Password**: `YOUR_API_KEY`

    Then use these credentials to send with PHPMailer:

    ```php theme={"theme":{"light":"github-light","dark":"vesper"}}
    <?php

    // Include Composer autoload file to load PHPMailer classes
    require __DIR__ . '/vendor/autoload.php';

    use PHPMailer\PHPMailer\PHPMailer;
    use PHPMailer\PHPMailer\Exception;

    $mail = new PHPMailer(true);

    try {
        $mail->isSMTP();
        $mail->Host = 'smtp.resend.com';
        $mail->SMTPAuth = true;
        $mail->Username = 'resend';
        $mail->Password = 're_xxxxxxxxx';
        $mail->SMTPSecure = 'tls';
        $mail->Port = 587;

        // Set email format to HTML
        $mail->isHTML(true);

        $mail->setFrom('onboarding@resend.dev');
        $mail->addAddress('delivered@resend.dev');
        $mail->Subject = 'Hello World';
        $mail->Body = '<strong>It works!</strong>';

        $mail->send();

        // Log the successfully sent message
        echo 'Email successfully sent';
    } catch (Exception $e) {
        // Log the detailed error for debugging
        error_log('Mailer Error: ' . $mail->ErrorInfo);
        // Show a generic error message to the user
        echo 'There was an error sending the email.';
    }
    ```
  </Step>
</Steps>

## Examples

<Card title="PHPMailer SMTP Example" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-phpmailer-smtp-example">
  See the full source code.
</Card>
