> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with FastAPI

> Learn how to send your first email using FastAPI and the Resend Python SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the Resend Python SDK.

    <CodeGroup>
      ```bash Pip theme={"theme":{"light":"github-light","dark":"vesper"}}
      pip install resend
      ```
    </CodeGroup>
  </Step>

  <Step title="Send email using HTML">
    The easiest way to send an email is by using the `html` parameter.

    ```py main.py theme={"theme":{"light":"github-light","dark":"vesper"}}
    import os
    from typing import Dict
    from fastapi import FastAPI
    import resend

    resend.api_key = os.environ["RESEND_API_KEY"]

    app = FastAPI()

    @app.post("/")
    def send_mail() -> Dict:
        params: resend.Emails.SendParams = {
            "from": "Acme <onboarding@resend.dev>",
            "to": ["delivered@resend.dev"],
            "subject": "hello world",
            "html": "<strong>it works!</strong>",
        }
        email: resend.Emails.SendResponse = resend.Emails.send(params)
        return email
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="FastAPI App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/fastapi_app.py">
    Full FastAPI web application
  </Card>

  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/basic_send.py">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/with_attachments.py">
    Send emails with file attachments
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/with_template.py">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/scheduled_send.py">
    Schedule emails for future delivery
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/audiences.py">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/domains.py">
    Create and manage sending domains
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/inbound.py">
    Receive and process inbound emails
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/double_optin_subscribe.py">
    Double opt-in subscription flow
  </Card>
</CardGroup>
