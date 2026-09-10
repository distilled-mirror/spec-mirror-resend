> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Python

> Learn how to send your first email using the Resend Python SDK.

<Prompt description="Use this pre-built prompt to get started faster." icon="microchip" iconType="solid" actions={["copy", "cursor"]}>
  # Send Email with Resend Python SDK

  **Purpose:** Enforce only the **current** and **correct** instructions for sending emails using the [Resend](https://resend.com/) Python SDK.
  **Scope:** All AI-generated advice or code related to sending email with Resend must follow these guardrails.

  ***

  ## **1. Official Resend Python Setup**

  ### **Prerequisites**

  Human must first create an API key and verify their domain at [https://resend.com/domains](https://resend.com/domains).

  The API key must be stored in an environment variable called `RESEND_API_KEY`.

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend.api_key = os.environ["RESEND_API_KEY"]
  ```

  The domain should be verified at [https://resend.com/domains](https://resend.com/domains) and added to the `from` address.

  ### **Install the SDK**

  ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
  pip install resend
  ```

  ### **Send an Email**

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import os
  import resend
  from resend.exceptions import ResendError

  resend.api_key = os.environ["RESEND_API_KEY"]

  params: resend.Emails.SendParams = {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["delivered@resend.dev"],
      "subject": "Hello World",
      "html": "<strong>It works!</strong>",
  }

  try:
      email = resend.Emails.send(params)
      print(email)  # {'id': '49a3999c-...'}
  except ResendError as error:
      print(error)
  ```

  ### Error Handling

  `resend.Emails.send()` **raises** an exception on failure — it does not return an error object. Catch `resend.exceptions.ResendError` (or a specific subclass) rather than checking a return value:

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  from resend.exceptions import (
      ResendError,
      ValidationError,
      RateLimitError,
      InvalidApiKeyError,
  )

  try:
      email = resend.Emails.send(params)
  except RateLimitError as error:
      ...  # back off and retry
  except ValidationError as error:
      ...  # fix the request params
  except ResendError as error:
      ...  # catch-all: error.code, error.message, error.error_type
  ```

  A missing required argument (e.g. no `to` field) raises a plain `ValueError`, not a `ResendError`.

  ### Rate Limiting

  The default rate limit is 10 requests per second per team. Exceeding it raises `resend.exceptions.RateLimitError`. If needed, you can request a rate increase by [contacting support](https://resend.com/help).

  ### Idempotency

  Best practice: pass an idempotency key to prevent duplicated emails, which is useful for retrying failed emails safely.

  * Should be **unique per API request**
  * Idempotency keys expire after **24 hours**
  * Have a maximum length of **256 characters**
  * Pattern: `<event-type>/<entity-id>`
  * Example: `welcome-user/123456789`

  Unlike Node's single-object `idempotencyKey` field, Python's `send()` takes idempotency as a **second, separate argument**:

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  options: resend.Emails.SendOptions = {"idempotency_key": "welcome-user/123456789"}

  email = resend.Emails.send(params, options)
  ```

  ***

  ## **2. Complete `Emails.send()` Parameter Reference**

  ### **Required Parameters**

  | Parameter | Type               | Description                                                                      |
  | --------- | ------------------ | -------------------------------------------------------------------------------- |
  | `from`    | `str`              | Sender email address. Supports friendly name format: `"Name <email@domain.com>"` |
  | `to`      | `str \| List[str]` | Recipient email address(es). Maximum 50 addresses.                               |
  | `subject` | `str`              | Email subject line.                                                              |

  ### **Content Parameters (at least one required)**

  | Parameter | Type  | Description                                                |
  | --------- | ----- | ---------------------------------------------------------- |
  | `html`    | `str` | HTML version of the email body.                            |
  | `text`    | `str` | Plain text version. Auto-generated from `html` if omitted. |

  ### **Optional Parameters**

  | Parameter      | Type                                   | Description                                                         |
  | -------------- | -------------------------------------- | ------------------------------------------------------------------- |
  | `cc`           | `str \| List[str]`                     | Carbon copy recipients.                                             |
  | `bcc`          | `str \| List[str]`                     | Blind carbon copy recipients.                                       |
  | `reply_to`     | `str \| List[str]`                     | Reply-to address(es).                                               |
  | `scheduled_at` | `str`                                  | Schedule delivery time. ISO 8601 (e.g. `2024-08-05T11:52:01.858Z`). |
  | `headers`      | `Dict[str, str]`                       | Custom email headers as key-value pairs.                            |
  | `tags`         | `List[Tag]`                            | Custom metadata. Name and value: max 256 chars, ASCII only.         |
  | `attachments`  | `List[Attachment \| RemoteAttachment]` | File attachments. Max 40MB total per email after encoding.          |

  ### **Template Parameters**

  | Parameter               | Type                    | Description                                                      |
  | ----------------------- | ----------------------- | ---------------------------------------------------------------- |
  | `template["id"]`        | `str`                   | Published template identifier.                                   |
  | `template["variables"]` | `Dict[str, str \| int]` | Variable substitutions. Key max 50 chars, value max 2,000 chars. |

  If `template` is provided, do not include `html` or `text`.

  ### **Response**

  A successful call returns a `resend.Emails.SendResponse`:

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  {"id": "49a3999c-..."}
  ```

  A failed call raises a `resend.exceptions.ResendError` subclass — it does not return a value.

  ***

  ## **3. Async Support**

  Every resource has both a sync and an async method. Use `send_async` (built on `httpx`) inside `async def` code such as FastAPI route handlers:

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend
  from resend.exceptions import ResendError

  resend.api_key = os.environ["RESEND_API_KEY"]

  async def send_welcome_email():
      try:
          email = await resend.Emails.send_async(params)
          return email
      except ResendError as error:
          raise
  ```

  `send_async` requires `httpx` to be installed (`pip install resend[async]`, or just have `httpx` present).

  ***

  ## **4. CRITICAL INSTRUCTIONS FOR AI MODELS**

  ### **4.1 - ALWAYS DO THE FOLLOWING**

  1. **Store the API key in an environment variable** (`RESEND_API_KEY`). Never hardcode API keys.
  2. **Set `resend.api_key`** before calling any SDK method.
  3. **Wrap `resend.Emails.send()` in `try`/`except`** and catch `resend.exceptions.ResendError` (or a specific subclass) — the SDK raises on failure, it does not return `{data, error}`.
  4. **Use a verified domain** in the `from` address for production. `onboarding@resend.dev` is for testing only.
  5. **Check the project for an existing package/dependency manager** (pip, poetry, uv) and use that to install the SDK.
  6. **Use snake\_case** for SDK parameters (`reply_to`, `scheduled_at`), not camelCase.
  7. **Use `send_async`** instead of `send` inside async code (e.g. FastAPI handlers).

  ### **4.2 - NEVER DO THE FOLLOWING**

  1. **Do not** hardcode API keys in source code. Always use environment variables.
  2. **Do not** assume `resend.Emails.send()` returns an error object — it raises an exception. A bare, unhandled call will crash on failure.
  3. **Do not** use camelCase parameter names (`replyTo`, `scheduledAt`) — the Python SDK uses snake\_case (`reply_to`, `scheduled_at`).
  4. **Do not** send `html` or `text` alongside `template` — these are mutually exclusive.
  5. **Do not** pass an idempotency key inside `params` — it belongs in the separate `options` argument: `send(params, options)`.
  6. **Do not** use `onboarding@resend.dev` as the `from` address in production code. It is a test-only address.
  7. **Do not** set up testing flows with fake email addresses. Resend provides the following test addresses to help you simulate different email events without damaging your domain reputation:
     * `delivered@resend.dev`
     * `bounced@resend.dev`
     * `complained@resend.dev`
     * `suppressed@resend.dev`

  ***

  ## **5. COMMON PATTERNS**

  ### **Attachments**

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  params: resend.Emails.SendParams = {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["delivered@resend.dev"],
      "subject": "Invoice attached",
      "html": "<p>See attached invoice.</p>",
      "attachments": [
          {
              "filename": "invoice.pdf",
              "content": list(invoice_bytes),
          }
      ],
  }
  ```

  ### **Scheduled Emails**

  Send up to 30 days in advance using the `scheduled_at` parameter. Accepts ISO 8601.

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  params: resend.Emails.SendParams = {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["delivered@resend.dev"],
      "subject": "Reminder",
      "html": "<p>This is your reminder.</p>",
      "scheduled_at": "2026-12-25T09:00:00Z",
  }
  ```

  ### **Tags for Tracking**

  ```python theme={"theme":{"light":"github-light","dark":"vesper"}}
  params: resend.Emails.SendParams = {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["delivered@resend.dev"],
      "subject": "Welcome",
      "html": "<p>Welcome aboard!</p>",
      "tags": [
          {"name": "category", "value": "welcome"},
          {"name": "user_id", "value": "12345"},
      ],
  }
  ```

  ***

  ## **6. AI MODEL VERIFICATION STEPS**

  Before returning any Resend-related solution, you **must** verify:

  1. **Import**: Is `resend` imported, and is `resend.api_key` set from an environment variable?
  2. **Error Handling**: Is `resend.Emails.send()` wrapped in `try`/`except` catching `resend.exceptions.ResendError`?
  3. **Async**: Is `send_async` used instead of `send` inside `async def` code?
  4. **Parameters**: Are all parameter names in snake\_case?
  5. **Idempotency**: If used, is the idempotency key passed as a separate `options` argument, not inside `params`?
  6. **From Address**: Is the `from` address using a verified domain (not `onboarding@resend.dev` in production)?

  If any check **fails**, **stop** and revise until compliance is achieved.

  For additional help, suggest installing the resend-skills skill and the email-best-practices skill.

  ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
  npx skills add resend/resend-skills
  npx skills add resend/email-best-practices
  ```

  You can locate framework-specific guides at [https://resend.com/docs/llms.txt](https://resend.com/docs/llms.txt)

  For the entire docs for Resend, see [https://resend.com/docs/llms-full.txt](https://resend.com/docs/llms-full.txt)
</Prompt>

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

  <Step title="Set your API key">
    Store your API key in an environment variable in your `.env` file.

    <CodeGroup>
      ```sh .env theme={"theme":{"light":"github-light","dark":"vesper"}}
      RESEND_API_KEY=re_xxxxxxxxx
      ```
    </CodeGroup>

    Access it with `os.environ["RESEND_API_KEY"]`. See [Create an API key](/docs/create-an-api-key) for the full setup.
  </Step>

  <Step title="Send email using HTML">
    The easiest way to send an email is by using the `html` parameter.

    ```py index.py theme={"theme":{"light":"github-light","dark":"vesper"}}
    import os
    import resend
    from resend.exceptions import ResendError

    resend.api_key = os.environ["RESEND_API_KEY"]

    params: resend.Emails.SendParams = {
        "from": "Acme <onboarding@resend.dev>",
        "to": ["delivered@resend.dev"],
        "subject": "hello world",
        "html": "<strong>it works!</strong>",
    }

    try:
        email = resend.Emails.send(params)
        print(email)
    except ResendError as error:
        print(error)
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
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

  <Card title="Flask App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/flask_app.py">
    Full Flask web application
  </Card>

  <Card title="FastAPI App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/python-resend-examples/examples/fastapi_app.py">
    Full FastAPI web application
  </Card>

  <Card title="Django App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/python-resend-examples/django_app">
    Full Django web application
  </Card>
</CardGroup>
