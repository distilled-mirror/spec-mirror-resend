> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# What's the difference between Opportunistic TLS vs Enforced TLS?

> Understand the different TLS configurations available.

Resend supports TLS 1.2, TLS 1.1 and TLS 1.0 for TLS connections.

There are two types of TLS configurations available:

* Opportunistic TLS
* Enforced TLS

## What is Opportunistic TLS?

Opportunistic TLS means that Resend always attempts to make a secure connection to the receiving mail server.

If the receiving server does not support TLS, the fallback is sending the message unencrypted.

## What is Enforced TLS?

Enforced TLS means that the email communication must use TLS no matter what.

If the receiving server does not support TLS, the email will not be sent.

## Is Enforced TLS better than Opportunistic TLS?

One strategy is not necessarily better than the other.

The decision is less about one option being safe and the other being unsafe, and more about one option being safe and the other being safer.

When you have Enforced TLS enabled, you might see an increase in bounce rates because some outdated mail servers do not support TLS.

So it's important to understand the different use cases for each configuration. If you're sending sensitive information like authentication emails, you might want to use Enforced TLS. If you're sending marketing emails, you might want to use Opportunistic TLS.

In simple terms, with Opportunistic TLS, delivery is more important than security. On the other hand, with Enforced TLS, security is more important than delivery.
