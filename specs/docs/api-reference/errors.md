> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Errors

> Troubleshoot problems with this comprehensive breakdown of all error codes.

## Error schema

Resend uses standard HTTP response codes for success and failure notifications, and errors are further classified by type.

### `invalid_idempotency_key`

* **Status:** 400
* **Message:** Idempotency keys, if present, must have between 1 and 256 characters.
* **Suggested action:** Retry with a valid idempotency key.

### `validation_error`

* **Status:** 400
* **Message:** An error was found with one or more fields in the request.
* **Suggested action:** The message will contain more details about what field and error were found.

### `missing_api_key`

* **Status:** 401
* **Message:** Missing API key in the authorization header.
* **Suggested action:** Include the following header in the request: `Authorization: Bearer YOUR_API_KEY`.

### `restricted_api_key`

* **Status:** 401
* **Message:** This API key is restricted to only send emails.
* **Suggested action:** Make sure the API key has `Full access` to perform actions other than sending emails.

### `email_above_quota`

* **Status:** 403
* **Message:** You can't retrieve this email's content because it was above quota when received.
* **Suggested action:** [Upgrade your plan](https://resend.com/settings/billing) to increase your quota.

### `invalid_permission`

* **Status:** 403
* **Message:** Access token is missing required scopes.
* **Suggested action:** Request an access token that includes the scopes required by this endpoint.

### `restricted_api_key`

* **Status:** 403
* **Message:** API key is not active
* **Suggested action:** Check the API key on the [API Keys page](https://resend.com/api-keys) and create a new one if needed.

### `suspended_api_key`

* **Status:** 403
* **Message:** This API key is suspended
* **Suggested action:** [Contact support](https://resend.com/contact) if you believe this is a mistake.

### `validation_error`

* **Status:** 403
* **Message:** You can only send testing emails to your own email address (`youremail@domain.com`). To send emails to other recipients, please verify a domain at resend.com/domains, and change the `from` address to an email using this domain.
* **Suggested action:** In [Resend's Domain page](https://resend.com/domains), add and verify a domain for which you have DNS access. This allows you to send emails to addresses beyond your own. [Learn more about resolving this error](/docs/knowledge-base/403-error-resend-dev-domain).

### `validation_error`

* **Status:** 403
* **Message:** The `domain.com` domain is not verified. Please, add and verify your domain.
* **Suggested action:** Make sure the domain in your API request's `from` field matches a domain you've verified in Resend. Update your API request to use your verified domain, or add and verify the domain you're trying to use. [Learn more about resolving this error](/docs/knowledge-base/403-error-domain-mismatch).

### `validation_error`

* **Status:** 403
* **Message:** The `example.com` domain has been registered already.
* **Suggested action:** Verify you are signed in to the correct Resend account and check whether a teammate already added the domain. If you still cannot access it, [contact support](https://resend.com/help). [Learn more about resolving this error](/docs/knowledge-base/domain-already-registered).

### `not_found`

* **Status:** 404
* **Message:** The requested endpoint does not exist.
* **Suggested action:** Change your request URL to match a valid API endpoint.

### `method_not_allowed`

* **Status:** 405
* **Message:** Method is not allowed for the requested path.
* **Suggested action:** Change your API endpoint to use a valid method.

### `concurrent_idempotent_requests`

* **Status:** 409
* **Message:** There is another request in progress with the same idempotency key.
* **Suggested action:** Try the request again later.

### `invalid_idempotent_request`

* **Status:** 409
* **Message:** This idempotency key has been used with this HTTP method and endpoint within the last 24 hours, but the request body was modified and doesn't match the original request.
* **Suggested action:** Change your idempotency key or payload.

### `resource_locked`

* **Status:** 409
* **Message:** Another request is already updating this resource.
* **Suggested action:** Retry the request after a short delay.

### `invalid_attachment`

* **Status:** 422
* **Message:** Attachment must have either a `content` or `path`.
* **Suggested action:** Attachments must either have a `content` (strings, Buffer, or Stream contents) or `path` to a remote resource (better for larger attachments).

### `invalid_parameter`

* **Status:** 422
* **Message:** The `parameter` must be a valid UUID.
* **Suggested action:** Check the value and make sure it's valid.

### `missing_required_field`

* **Status:** 422
* **Message:** The request body is missing one or more required fields.
* **Suggested action:** Check the error message to see the list of missing fields.

### `missing_required_parameter`

* **Status:** 422
* **Message:** The request is missing one or more required parameters.
* **Suggested action:** Check the error message to see the list of missing parameters.

### `daily_quota_exceeded`

* **Status:** 429
* **Message:** You have exceeded your daily email sending quota.
* **Suggested action:** [Upgrade your plan](https://resend.com/settings/billing) to remove the daily quota limit or wait until 24 hours have passed. Both sent and received emails count towards this quota.

### `monthly_quota_exceeded`

* **Status:** 429
* **Message:** You have exceeded your monthly email sending quota.
* **Suggested action:** [Upgrade your plan](https://resend.com/settings/billing) to increase the monthly email quota. Both sent and received emails count towards this quota.

### `rate_limit_exceeded`

* **Status:** 429
* **Message:** Too many requests. Please limit the number of requests per second. Or [contact support](https://resend.com/contact) to increase rate limit.
* **Suggested action:** Read the [response headers](/docs/api-reference/introduction#rate-limit) and reduce the rate at which you request the API. This can be done by introducing a queue mechanism or reducing the number of concurrent requests per second. If you have specific requirements, [contact support](https://resend.com/contact) to request a rate increase.

### `application_error`

* **Status:** 500
* **Message:** An unexpected error occurred.
* **Suggested action:** Try the request again later. If the error does not resolve, check our [status page](https://resend-status.com) for service updates.

### `service_unavailable`

* **Status:** 503
* **Message:** API is temporarily unavailable
* **Suggested action:** Try the request again later. Check our [status page](https://resend-status.com) for service updates.
