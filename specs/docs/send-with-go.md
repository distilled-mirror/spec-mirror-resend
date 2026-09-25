> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Go

> Learn how to send your first email using the Resend Go SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the Resend Go SDK.

    <CodeGroup>
      ```bash bash theme={"theme":{"light":"github-light","dark":"vesper"}}
      go get github.com/resend/resend-go/v4
      ```
    </CodeGroup>
  </Step>

  <Step title="Send email using HTML">
    The easiest way to send an email is by using the `html` parameter.

    ```Go main.go theme={"theme":{"light":"github-light","dark":"vesper"}}
    package main

    import (
    	"fmt"

    	"github.com/resend/resend-go/v4"
    )

    func main() {
        client := resend.NewClient("re_xxxxxxxxx")

        params := &resend.SendEmailRequest{
            From:    "Acme <onboarding@resend.dev>",
            To:      []string{"delivered@resend.dev"},
            Html:    "<strong>hello world</strong>",
            Subject: "Hello from Golang",
            Cc:      []string{"cc@example.com"},
            Bcc:     []string{"bcc@example.com"},
            ReplyTo: "replyto@example.com",
        }

        sent, err := client.Emails.Send(params)
        if err != nil {
            fmt.Println(err.Error())
            return
        }
        fmt.Println(sent.Id)
    }
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/basic_send">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/with_attachments">
    Send emails with file attachments
  </Card>

  <Card title="Inline Images (CID)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/with_cid_attachments">
    Embed inline images using CID
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/with_template">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/scheduled_send">
    Schedule emails for future delivery
  </Card>

  <Card title="Prevent Threading" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/prevent_threading">
    Prevent email threading on Gmail
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/audiences">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/domains">
    Create and manage sending domains
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/inbound">
    Receive and process inbound emails
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/double_optin">
    Double opt-in subscription flow
  </Card>

  <Card title="Chi App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/chi_app">
    Full Chi web framework application
  </Card>

  <Card title="Gin App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/go-resend-examples/gin_app">
    Full Gin web framework application
  </Card>
</CardGroup>
