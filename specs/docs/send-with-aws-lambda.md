> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with AWS Lambda

> Learn how to send your first email using AWS Lambda.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key.md)
* A [verified domain](/docs/add-a-domain.md)

## Guide

**1. Create an AWS Lambda function**

Go to [aws.amazon.com](https://aws.amazon.com) and create a new Lambda function using the Node.js 20.x or later runtime.

![AWS Lambda - New Function](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/aws-lambda-new-function.png?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=324a1181f685affebb1f50b18765538c)

**2. Edit the handler function**

Paste the following code into the browser editor:

```js index.mjs theme={"theme":{"light":"github-light","dark":"vesper"}}
const RESEND_API_KEY = 're_xxxxxxxxx';

export const handler = async (event) => {
  const res = await fetch('https://api.resend.com/emails', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${RESEND_API_KEY}`,
    },
    body: JSON.stringify({
      from: 'Acme <onboarding@resend.dev>',
      to: ['delivered@resend.dev'],
      subject: 'hello world',
      html: '<strong>it works!</strong>',
    }),
  });

  if (res.ok) {
    const data = await res.json();

    return {
      statusCode: 200,
      body: data,
    };
  }
};
```

**3. Deploy and send email**

Click on `Deploy` and then `Test` at the top of the screen.

![AWS Lambda - Edit Function](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/aws-lambda-edit-function.png?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=0393dc19bce3c93881bf4b433024c40b)

## Examples

> **[AWS Lambda Example](https://github.com/resend/resend-aws-lambda-example)**
>
> See the full source code.
