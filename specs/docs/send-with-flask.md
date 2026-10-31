> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Flask

> Learn how to send your first email using Flask and the Resend Python SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

## Guide

**1. Install**

Get the Resend Python SDK.

```bash Pip theme={"theme":{"light":"github-light","dark":"vesper"}}
pip install resend
```

**2. Send email using HTML**

The easiest way to send an email is by using the `html` parameter.

```py index.py theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend
import os
from flask import Flask, jsonify

resend.api_key = os.environ["RESEND_API_KEY"]

app = Flask(__name__)


@app.route("/")
def index():
    params: resend.Emails.SendParams = {
        "from": "Acme <onboarding@resend.dev>",
        "to": ["delivered@resend.dev"],
        "subject": "hello world",
        "html": "<strong>it works!</strong>",
    }

    r = resend.Emails.send(params)
    return jsonify(r)


if __name__ == "__main__":
    app.run()
```

## Examples

> [card] [Flask App](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/flask_app.py)
>
> Full Flask web application

> [card] [Basic Send](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/basic_send.py)
>
> Basic email sending

> [card] [Attachments](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/with_attachments.py)
>
> Send emails with file attachments

> [card] [Templates](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/with_template.py)
>
> Send emails using Resend hosted templates

> [card] [Scheduling](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/scheduled_send.py)
>
> Schedule emails for future delivery

> [card] [Audiences](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/audiences.py)
>
> Manage contacts and audiences

> [card] [Domains](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/domains.py)
>
> Create and manage sending domains

> [card] [Inbound Webhooks](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/inbound.py)
>
> Receive and process inbound emails

> [card] [Double Opt-in](https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/double_optin_subscribe.py)
>
> Double opt-in subscription flow
