> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Cancel Automation Run

> Cancel a single automation run.

Cancelling a run skips its remaining steps. Emails the run already sent stay sent, and the Automation stays enabled. To disable the Automation and cancel all of its runs in progress, [stop the Automation](https://resend.com/docs/api-reference/automations/stop-automation.md) instead.

You can cancel a run that's `running` or `quota_exceeded`. Cancelling a run that's `completed`, `failed`, or `skipped` returns a `422` `validation_error`. Cancelling a run that's already cancelled succeeds and changes nothing.

A cancelled run was stopped on purpose, not by an error. Steps that already finished stay finished, and the remaining steps show as `skipped`. Learn more about [cancelled runs](https://resend.com/docs/dashboard/automations/runs.md#cancelled-runs).

## Path Parameters

The Automation ID.

The Automation run ID.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.automations.runs.cancel({
  automationId: 'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
  runId: 'a1b2c3d4-e5f6-7890-abcd-ef1234567890',
});
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/automations/c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd/runs/a1b2c3d4-e5f6-7890-abcd-ef1234567890/cancel' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "automation_run",
  "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "status": "cancelled"
}
```
