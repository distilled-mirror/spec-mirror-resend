> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails using Django with SMTP

> Learn how to integrate Django with Resend SMTP.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)
* Install `virtualenv` by running `pip install virtualenv`

## Guide

<Steps>
  <Step title="Setup your environment">
    Create and activate your new virtualenv.

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    virtualenv venv
    source venv/bin/activate
    ```

    Install dependencies.

    ```sh theme={"theme":{"light":"github-light","dark":"vesper"}}
    pip install -r requirements.txt
    ```

    Set your `RESEND_API_KEY` environment variable by running.

    ```sh theme={"theme":{"light":"github-light","dark":"vesper"}}
    export RESEND_API_KEY="re_xxxxxxxxx"
    ```
  </Step>

  <Step title="Send email using Django's SMTP EmailMessage">
    Set the necessary attributes in your `settings.py` file.

    ```py theme={"theme":{"light":"github-light","dark":"vesper"}}
    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    RESEND_SMTP_PORT = 587
    RESEND_SMTP_USERNAME = 'resend'
    RESEND_SMTP_HOST = 'smtp.resend.com'
    ```

    Use Django's `get_connection` and `EmailMessage`

    ```py theme={"theme":{"light":"github-light","dark":"vesper"}}
    import os
    from django.conf import settings
    from django.http import JsonResponse
    from django.core.mail import EmailMessage, get_connection

    # Sample Django view
    def index(request):

        subject = "Hello from Django SMTP"
        recipient_list = ["delivered@resend.dev"]
        from_email = "onboarding@resend.dev"
        message = "<strong>it works!</strong>"

        with get_connection(
            host=settings.RESEND_SMTP_HOST,
            port=settings.RESEND_SMTP_PORT,
            username=settings.RESEND_SMTP_USERNAME,
            password=os.environ["RESEND_API_KEY"],
            use_tls=True,
            ) as connection:
                r = EmailMessage(
                      subject=subject,
                      body=message,
                      to=recipient_list,
                      from_email=from_email,
                      connection=connection).send()
        return JsonResponse({"status": "ok"})
    ```
  </Step>
</Steps>

## Examples

<Card title="Django SMTP Example" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-django-smtp-example">
  See the full source code.
</Card>
