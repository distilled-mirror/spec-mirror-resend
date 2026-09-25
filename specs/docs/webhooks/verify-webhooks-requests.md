> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Verify Webhooks Requests

> Learn how to use the signing secret to verify your webhooks.

Webhook signing secrets are used to validate the payload data sent to your application from Resend. You can find the signing secret on the webhook details page.

<img alt="Signing Secret" src="https://mintcdn.com/resend/qZ1nhePh39wY_UO4/images/webhooks-secret-1.png?fit=max&auto=format&n=qZ1nhePh39wY_UO4&q=85&s=fa5955e5da08d6263850dfd024c642bb" width="3318" height="2088" data-path="images/webhooks-secret-1.png" />

Calls to [create](/docs/api-reference/webhooks/create-webhook), [retrieve](/docs/api-reference/webhooks/get-webhook), or [list](/docs/api-reference/webhooks/list-webhooks) webhooks will also return the signing secret in the response body.

## How to verify webhook requests

To verify the webhook request, you can use the Resend SDK, as in the example below.

<Tip>
  Make sure that you're using the raw request body when verifying webhooks. The
  cryptographic signature is sensitive to even the slightest change. Some
  frameworks parse the request as JSON and then stringify it, and this will also
  break the signature verification.
</Tip>

```js theme={"theme":{"light":"github-light","dark":"vesper"}}
export async function POST(req: NextRequest) {
  try {
    const payload = await req.text();

    // Throws an error if the webhook is invalid
    // Otherwise, returns the parsed payload object
    const result = resend.webhooks.verify({
      payload,
      headers: {
        id: req.headers['svix-id'],
        timestamp: req.headers['svix-timestamp'],
        signature: req.headers['svix-signature'],
      },
      webhookSecret: process.env.RESEND_WEBHOOK_SECRET,
    });

    // Handle the result after validating it
  } catch {
    return new NextResponse('Invalid webhook', { status: 400 });
  }
}
```

Alternatively, you can manually use the Svix libraries and manually pass it the headers, body, and webhook secret. [Learn more and view all supported languages here.](https://docs.svix.com/receiving/verifying-payloads/how)

To verify manually, start by installing the Svix libaries.

<CodeGroup>
  ```sh npm theme={"theme":{"light":"github-light","dark":"vesper"}}
  npm install svix
  ```

  ```sh yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
  yarn add svix
  ```

  ```sh pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
  pnpm add svix
  ```

  ```sh bun theme={"theme":{"light":"github-light","dark":"vesper"}}
  bun add svix
  ```
</CodeGroup>

Then, verify the webhooks using the code below. The payload is the raw (string) body of the request, and the headers are the headers passed in the request.

```js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Webhook } from 'svix';

const secret = process.env.WEBHOOK_SECRET;

// These were all sent from the server
const headers = {
  'svix-id': 'msg_p5jXN8AQM9LWM0D4loKWxJek',
  'svix-timestamp': '1614265330',
  'svix-signature': 'v1,g0hM9SsE+OTPJTGt/tmIKtSyZlE3uFJELVlNIOLJ1OE=',
};
const payload = '{"test": 2432232314}';

const wh = new Webhook(secret);
// Throws on error, returns the verified content on success
wh.verify(payload, headers);
```

If you prefer, you can also [manually verify the headers as well.](https://docs.svix.com/receiving/verifying-payloads/how-manual)

## Why verify webhooks

Webhooks are vulnerable because attackers can send fake HTTP POST requests to endpoints, pretending to be legitimate services. This can lead to security risks or operational issues.

To mitigate this, each webhook and its metadata are signed with a unique key specific to the endpoint. This signature helps verify the source of the webhook, allowing only authenticated webhooks to be processed.

Another security concern is replay attacks, where intercepted valid payloads, complete with their signatures, are resent to endpoints. These payloads would pass the signature verification and be executed, posing a potential security threat.

## API Reference

For complete API documentation, see the [Webhooks API reference](/docs/api-reference/webhooks/create-webhook).
