> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retries and Replays

> Learn how to use the retries and replays to handle webhook failures.

## Automatic Retries

Resend attempts to deliver each webhook message based on a schedule with exponential backoff.

Each message is attempted based on the following schedule, where each period is started following the failure of the preceding attempt:

* Immediately
* 5 seconds
* 5 minutes
* 30 minutes
* 2 hours
* 5 hours
* 10 hours
* 10 hours (in addition to the previous)

For example, an attempt that fails three times before eventually succeeding will be delivered roughly 35 minutes and 5 seconds following the first attempt.

If an endpoint is removed or disabled, delivery attempts to the endpoint will be disabled as well.

To see when a message will be retried next, check the webhook message details in the dashboard.

## Failure notifications

When a webhook endpoint starts failing to receive events, Resend sends an email notification to your team. The email includes the endpoint URL, the time of the last failed attempt, and the last HTTP response status code.

If the endpoint continues to fail, Resend will eventually disable it automatically and send a second notification to let you know. Once your endpoint is back up, you can re-enable it from the [Webhooks](https://resend.com/webhooks) page in the dashboard.

## Manual Replays

If a webhook message fails, you can manually replay it.

You can replay both `failed` and `succeeded` webhook messages.

<img alt="Replay Webhook" src="https://mintcdn.com/resend/qZ1nhePh39wY_UO4/images/webhooks-replay-1.jpg?fit=max&auto=format&n=qZ1nhePh39wY_UO4&q=85&s=aeae9936eeea92d71da580af9f82cbb5" width="1476" height="448" data-path="images/webhooks-replay-1.jpg" />

Here's how to replay a webhook message:

1. Go to the [Webhooks](https://resend.com/webhooks) page
2. Navigate to the Webhook Endpoint you are using
3. Go to the Webhook Message you want to replay
4. Click on the "Replay" button
