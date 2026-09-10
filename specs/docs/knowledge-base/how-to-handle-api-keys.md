> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to handle API keys

> Learn how to handle API keys securely.

## Best Practices

Handle your API keys securely. Don't share your API key with others or expose it in the browser or other client-side code.

Here are some general guidelines:

* Store API keys in environment variables.
* Never commit API keys to version control.
* Never hard-code API keys in your code or share them publicly.
* Rotate API keys regularly. If an API key hasn't been used in the last 30 days, consider deleting it to keep your account secure.

<Info>You can view an API key only once after you create it.</Info>

<Warning>
  If a key has already been exposed or used without your authorization, see [how
  to handle a leaked API key](/docs/knowledge-base/how-to-handle-a-leaked-api-key).
</Warning>

## Key Rotation

Resend API keys don't expire automatically. Keys remain valid until you manually delete them. Resend includes no built-in expiration date or automatic rotation mechanism, but it's a good security practice to rotate keys regularly.

To rotate an API key:

1. **Create a new key** in the [**API keys** Dashboard page](https://resend.com/api-keys) or [via the API](/docs/api-reference/api-keys/create-api-key) with the same permission level and domain scope as the key you're replacing.
2. **Update your services** to use the new key. Deploy the change to all environments that reference the old key.
3. **Verify the new key is working** by [filtering by API key on the **Logs** Dashboard page](https://resend.com/logs) and checking for recent requests.
4. **Delete the old key** once you've confirmed the new key is active across all services.

<Warning>
  Don't delete the old key before the new key is deployed everywhere. Both keys
  will work simultaneously, so ensure your new key is working before deleting
  your old key so you don't experience downtime during the transition. You can
  programmatically [create](/docs/api-reference/api-keys/create-api-key),
  [list](/docs/api-reference/api-keys/list-api-keys), and
  [delete](/docs/api-reference/api-keys/delete-api-key) API keys to rotate keys.
</Warning>

Rotate keys at least every 90 days, or immediately if you suspect a key has been compromised. Resend flags keys unused for 30 or more days in the Dashboard to help you identify keys to review or delete.

If you already know a key has leaked, delete it now rather than rotating it on a schedule. The steps to contain the incident are in [how to handle a leaked API key](/docs/knowledge-base/how-to-handle-a-leaked-api-key).
