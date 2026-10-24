> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Go

> Learn how to send your first email using the Resend Go SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

## Guide

**1. Install**

Get the Resend Go SDK.

```bash bash theme={"theme":{"light":"github-light","dark":"vesper"}}
go get github.com/resend/resend-go/v4
```

**2. Send email using HTML**

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

## Examples

> **[Basic Send](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/basic_send)**
>
> Basic email sending

> **[Attachments](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/with_attachments)**
>
> Send emails with file attachments

> **[Inline Images (CID)](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/with_cid_attachments)**
>
> Embed inline images using CID

> **[Templates](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/with_template)**
>
> Send emails using Resend hosted templates

> **[Scheduling](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/scheduled_send)**
>
> Schedule emails for future delivery

> **[Prevent Threading](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/prevent_threading)**
>
> Prevent email threading on Gmail

> **[Audiences](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/audiences)**
>
> Manage contacts and audiences

> **[Domains](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/domains)**
>
> Create and manage sending domains

> **[Inbound Webhooks](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/inbound)**
>
> Receive and process inbound emails

> **[Double Opt-in](https://github.com/resend/resend-examples/tree/main/go-resend-examples/examples/double_optin)**
>
> Double opt-in subscription flow

> **[Chi App](https://github.com/resend/resend-examples/tree/main/go-resend-examples/chi_app)**
>
> Full Chi web framework application

> **[Gin App](https://github.com/resend/resend-examples/tree/main/go-resend-examples/gin_app)**
>
> Full Gin web framework application
