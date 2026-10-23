> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Deno Deploy

> Learn how to send your first email using Deno Deploy.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key.md)
* A [verified domain](/docs/add-a-domain.md)

## Guide

**1. Create a Deno Deploy project**

Go to [dash.deno.com/projects](https://dash.deno.com/projects) and create a new playground project.

![Deno Deploy - New Project](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/deno-deploy-new-project.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=634d342d6e542f4c82eb9c013bfcc817)

**2. Edit the handler function**

Paste the following code into the browser editor:

```ts main.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'npm:resend';

const resend = new Resend('re_123456789');

Deno.serve(async () => {
  try {
    const response = await resend.emails.send({
      from: 'Acme <onboarding@resend.dev>',
      to: ['delivered@resend.dev'],
      subject: 'Hello World',
      html: '<strong>It works!</strong>',
    });

    return new Response(JSON.stringify(response), {
      status: response.error ? 500 : 200,
      headers: {
        'Content-Type': 'application/json',
      },
    });
  } catch (error) {
    console.error(error);
    return new Response(null, {
      status: 500,
    });
  }
});
```

**3. Deploy and send email**

Click on `Save & Deploy` at the top of the screen.

![Deno Deploy - Playground](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/deno-deploy-playground.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=fb62c969114e48e5401fecc67f5a4d76)

## Examples

> **[Deno Deploy Example](https://github.com/resend/resend-deno-deploy-example)**
>
> See the full source code.
