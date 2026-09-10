> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Steps

> Steps and their properties in Automation workflows.

## How it works

Steps are the building blocks of Automation workflows. They define the actions that will be executed when the Automation runs.

The following steps are available:

* [Trigger](/docs/dashboard/automations/trigger)
* [Condition](/docs/dashboard/automations/condition)
* [Delay](/docs/dashboard/automations/delay)
* [Wait for Event](/docs/dashboard/automations/wait-for-event)
* [Send Email](/docs/dashboard/automations/send-email)
* [Add to Segment](/docs/dashboard/automations/add-to-segment)
* [Contact Update](/docs/dashboard/automations/contact-update)
* [Contact Delete](/docs/dashboard/automations/contact-delete)

## Step properties

Every step in an automation has the following base properties:

<ParamField body="key" type="string" required>
  A unique identifier for the step. Used in connection definitions to connect
  steps.
</ParamField>

<ParamField body="type" type="string" required>
  The type of step. Possible values:

  * `trigger`
  * `send_email`
  * `delay`
  * `wait_for_event`
  * `condition`
  * `contact_update`
  * `contact_delete`
  * `add_to_segment`
</ParamField>

<ParamField body="config" type="object" required>
  The configuration object for the step. The shape depends on the step `type`.
</ParamField>

Below is a list of all the possible step types and their configurations.

### `trigger`

The trigger step starts the automation when a matching event is received.

<ParamField body="config.event_name" type="string" required>
  The name of the event that triggers the automation.
</ParamField>

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "start",
  "type": "trigger",
  "config": {
    "event_name": "user.created"
  }
}
```

### `send_email`

Sends an email using a template.

<ParamField body="config.template" type="object" required>
  The published template to send. Provide `id` and optionally `variables`.

  <Expandable defaultOpen title="properties">
    <ParamField body="config.template.id" type="string" required>
      The ID or alias of the template to send.
    </ParamField>

    <ParamField body="config.template.variables" type="object">
      A key-value map of template variables. Each value can be a static string or a variable reference object (`{ "var": "event.fieldName" }`) that resolves dynamically from the `event.*`, `contact.*`, or `wait_events.*` namespaces.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="config.from" type="string">
  The sender email address.

  If provided, this value will override the template's default value.
</ParamField>

<ParamField body="config.subject" type="string">
  The email subject line.

  If provided, this value will override the template's default value.
</ParamField>

<ParamField body="config.reply_to" type="string">
  Reply-to email address.

  If provided, this value will override the template's default value.
</ParamField>

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "welcome",
  "type": "send_email",
  "config": {
    "template": {
      "id": "062f8ef4-fbfa-44f1-b5e0-ff8e1e8ffa96",
      "variables": {
        "name": { "var": "event.firstName" }
      }
    },
    "from": "hello@example.com",
    "subject": "Welcome!",
    "reply_to": "support@example.com"
  }
}
```

### `delay`

Pauses execution for a specified duration.

<ParamField body="config.duration" type="string" required>
  The delay duration in natural language (e.g. `"1 hour"`, `"3 days"`). Maximum:
  30 days.
</ParamField>

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "wait_1_hour",
  "type": "delay",
  "config": {
    "duration": "1 hour"
  }
}
```

### `wait_for_event`

Pauses execution until a specific event is received or a timeout is reached.

<ParamField body="config.event_name" type="string" required>
  The name of the event to wait for.
</ParamField>

<ParamField body="config.timeout" type="string">
  The maximum time to wait before timing out (e.g. `"3 days"`, `"1 hour"`).
  Maximum: 30 days.
</ParamField>

<ParamField body="config.filter_rule" type="object">
  An optional rule object to filter incoming events.
</ParamField>

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "wait_for_purchase",
  "type": "wait_for_event",
  "config": {
    "event_name": "purchase.completed",
    "timeout": "3 days"
  }
}
```

### `condition`

Branches the workflow based on rules. Condition configs can be a single rule or a logical group (`and`/`or`) of rules.

<ParamField body="config.type" type="string" required>
  The type of condition node. Possible values:

  * `rule`
  * `and`
  * `or`
</ParamField>

For `rule` type:

<ParamField body="config.field" type="string" required>
  The field to evaluate. Must use the `event.` or `contact.` namespace prefix
  (e.g., `event.amount`, `contact.email`).
</ParamField>

<ParamField body="config.operator" type="string" required>
  The comparison operator. Possible values:

  * `eq`: equals
  * `neq`: not equals
  * `gt`: greater than
  * `gte`: greater than or equal to
  * `lt`: less than
  * `lte`: less than or equal to
  * `contains`: contains a given value
  * `starts_with`: starts with a given value
  * `ends_with`: ends with a given value
  * `exists`: field exists
  * `is_empty`: field is empty
</ParamField>

<ParamField body="config.value" type="string | number | boolean | null">
  The value to compare against. Not required for `exists` and `is_empty`
  operators.
</ParamField>

For `and` / `or` types:

<ParamField body="config.rules" type="object[]" required>
  An array of nested condition config objects. Must contain at least one item.
</ParamField>

Single rule example:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "check_plan",
  "type": "condition",
  "config": {
    "type": "rule",
    "field": "event.plan",
    "operator": "eq",
    "value": "pro"
  }
}
```

Use `and` or `or` to combine multiple rules into a single branch:

```json {5-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "check_plan_and_amount",
  "type": "condition",
  "config": {
    "type": "and",
    "rules": [
      {
        "type": "rule",
        "field": "event.plan",
        "operator": "eq",
        "value": "pro"
      },
      {
        "type": "rule",
        "field": "event.amount",
        "operator": "gte",
        "value": 100
      }
    ]
  }
}
```

### `contact_update`

Updates a contact's fields. Each field value can be either a hardcoded value or a dynamic variable reference using the `{ var: '...' }` syntax.

Variable references use dot-notation with one of these scopes:

* `event.*`: references a field from the triggering event payload (e.g., `event.firstName`).
* `contact.*`: references a field from the current contact (e.g., `contact.last_name`, `contact.properties.company`).

<ParamField body="config.first_name" type="string | object">
  The contact's first name. Accepts a hardcoded string or a variable reference.
</ParamField>

<ParamField body="config.last_name" type="string | object">
  The contact's last name. Accepts a hardcoded string or a variable reference.
</ParamField>

<ParamField body="config.unsubscribed" type="boolean | object">
  The contact's unsubscribed status. Accepts a boolean or a variable reference.
</ParamField>

<ParamField body="config.properties" type="object">
  A map of custom contact properties to update. Keys correspond to your [Contact
  Custom Properties](/docs/dashboard/audiences/properties). Each value can be a
  hardcoded value (string, number, boolean) or a variable reference.
</ParamField>

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "update_contact",
  "type": "contact_update",
  "config": {
    "properties": {
      "company": { "var": "event.company" },
      "vip": true
    }
  }
}
```

### `contact_delete`

Deletes the contact from the audience. This step does not require any configuration fields. Pass an empty object `{}` as the config.

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "remove_contact",
  "type": "contact_delete",
  "config": {}
}
```

### `add_to_segment`

Adds the contact to a segment.

<ParamField body="config.segment_id" type="string" required>
  The ID of the segment to add the contact to.
</ParamField>

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "add_to_vip",
  "type": "add_to_segment",
  "config": {
    "segment_id": "83a1e324-26dc-47eb-9b28-ba8b6d1fe808"
  }
}
```
