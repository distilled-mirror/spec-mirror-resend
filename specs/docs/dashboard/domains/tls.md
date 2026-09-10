> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Configure Transport Layer Security (TLS)

> Learn how to configure TLS for your verified domain in Resend.

## Configure Enforced Transport Layer Security (TLS)

Resend supports TLS 1.2, TLS 1.1 and TLS 1.0 for TLS connections, but only requires TLS for sending when Enforced TLS is configured.

By default, Resend will attempt to make a secure connection, but will fall back to sending messages unencrypted when the receiving server does not support TLS. This is known as Opportunistic TLS.

You can instead configure Enforced TLS in the Resend Dashboard under the **Configuration** tab or with the [Domains API](/docs/api-reference/domains/create-domain) or with [a domains CLI command](/docs/cli#domains). This means that if the receiving server does not support TLS, your email will not be sent.

Learn more about [Opportunistic TLS vs Enforced TLS](/docs/knowledge-base/whats-the-difference-between-opportunistic-tls-vs-enforced-tls).
