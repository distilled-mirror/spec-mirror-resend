> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage Labels

> Learn how to organize threads with inbox labels.

A label is a named, colored tag that you can apply to threads to keep an inbox organized. Labels belong to a single inbox, and a thread can have more than one label.

## Create a label

### Using the dashboard

**1. Open an inbox and click the **Settings** button.**

**2. Select the **Labels** tab.**

**3. Click **Add label**.**

**4. Enter a name for the label and choose a color.**

New labels start with a random color.

**5. Save the label.**

Press <kbd>Enter</kbd> or click the check button.

You can also create a label while applying it to a thread. Type the new name into the **Label as** menu and choose **Create label**.

An inbox can have up to 100 labels, and each label name must be unique within the inbox, ignoring case.

### Using the API

The color is a `#RRGGBB` hex code. If you leave it out, Resend picks one for you.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.labels.create({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  name: 'Urgent',
  color: '#E93D82',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->labels->create('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'name' => 'Urgent',
  'color' => '#E93D82',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Labels.CreateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "name": "Urgent",
  "color": "#E93D82",
}

resend.Inboxes.Labels.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "name": "Urgent",
  "color": "#E93D82",
}

Resend::Inboxes::Labels.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.CreateInboxLabelRequest{
		Name:  "Urgent",
		Color: "#E93D82",
	}

	client.Inboxes.Labels.Create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::CreateInboxLabelOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let label = CreateInboxLabelOptions::new("Urgent").with_color("#E93D82");

  let _label = resend
    .inboxes
    .create_label("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", label)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.CreateInboxLabelOptions;
import com.resend.services.inboxes.model.CreateInboxLabelResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        CreateInboxLabelOptions params = CreateInboxLabelOptions.builder()
                .name("Urgent")
                .color("#E93D82")
                .build();

        CreateInboxLabelResponseSuccess data = resend.inboxes().labels().create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxLabelCreateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxLabelCreateData()
    {
        Name = "Urgent",
        Color = "#E93D82",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/labels' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "name": "Urgent",
  "color": "#E93D82"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes labels create \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --name Urgent \
  --color '#E93D82'
```

## Apply labels to threads

In the Dashboard, open a thread or hover over it in the thread list and click **Label as**, or press <kbd>L</kbd>. Check the labels you want to apply and uncheck the ones you want to remove. To label many threads at once, select them in the list and use **Label as** in the bar at the bottom of the list.

You can also remove a label from a thread by clicking the **×** on the label under the thread subject.

> [!TIP]
>
> **Move to**, or <kbd>V</kbd>, lists your labels alongside your folders.
> Choosing a label from **Move to** applies the label and archives the thread in
> one step, which is useful for clearing your inbox.

You can also change a thread's labels via the API, SDKs, or CLI:

* [Add thread labels](https://resend.com/docs/api-reference/inboxes/add-thread-labels.md) applies up to 10 labels and keeps the labels already on the thread.
* [Set thread labels](https://resend.com/docs/api-reference/inboxes/set-thread-labels.md) replaces every label on the thread. Pass an empty list to remove them all.
* [Remove thread label](https://resend.com/docs/api-reference/inboxes/remove-thread-label.md) removes a single label from the thread.

Removing a label from a thread does not delete the label.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.labels.add({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  labels: ['7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->labels->add(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  [
    'labels' => ['7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'],
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.Labels.AddParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "labels": ["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"],
}

resend.Inboxes.Threads.Labels.add(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "labels": ["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"],
}

Resend::Inboxes::Threads::Labels.add(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.AddInboxThreadLabelsRequest{
		Labels: []string{"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"},
	}

	client.Inboxes.Threads.Labels.Add(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		params,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _labels = resend
    .inboxes
    .add_thread_labels(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      &["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"],
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.AddInboxThreadLabelsOptions;
import com.resend.services.inboxes.model.AddInboxThreadLabelsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        AddInboxThreadLabelsOptions params = AddInboxThreadLabelsOptions.builder()
                .labels("7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34")
                .build();

        AddInboxThreadLabelsResponseSuccess data = resend.inboxes().threads().addLabels(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxThreadLabelAddAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new List<Guid> { new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" ) }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/labels' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "labels": ["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"]
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads labels add \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --thread-id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --labels 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34
```

The [inbox agent](https://resend.com/docs/dashboard/inboxes/agent.md) can also apply your existing labels to threads based on your instructions.

## Filter threads by label

In the Dashboard, select a label in the left rail or from the folder switcher to see only the threads with that label. You can also click a label on a thread, or use the `label:` operator in search.

Labels also power the **Grouped list** and card-based [inbox views](https://resend.com/docs/dashboard/inboxes/manage-inboxes.md#edit-an-inbox), which group threads by label.

To filter threads by label via the API, pass a comma-separated list of label IDs in the `labels` parameter when you [list](https://resend.com/docs/api-reference/inboxes/list-threads.md) or [search](https://resend.com/docs/api-reference/inboxes/search-threads.md) threads.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  labels: ['7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->list('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'labels' => ['7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'],
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.ListParams = {
  "labels": ["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"],
}

resend.Inboxes.Threads.list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "labels": ["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"],
}

Resend::Inboxes::Threads.list(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.ListInboxThreadsOptions{
		Labels: []string{"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"},
	}

	client.Inboxes.Threads.List("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, types::ListInboxThreadsOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let filters = ListInboxThreadsOptions::new().with_labels(["7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"]);

  let _threads = resend
    .inboxes
    .list_threads(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      filters,
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxThreadsParams;
import com.resend.services.inboxes.model.ListInboxThreadsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxThreadsParams params = ListInboxThreadsParams.builder()
                .labels("7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34")
                .build();

        ListInboxThreadsResponseSuccess data = resend.inboxes().threads().list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadListAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxThreadListQuery()
    {
        Labels = new List<Guid> { new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" ) },
    }
);
Console.WriteLine( "Nr Threads={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads?labels=7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads list \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --labels 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34
```

When you filter by label, threads in the `inbox`, `archive`, and `sent` folders are included by default.

## Edit a label

In the **Labels** tab of the inbox settings, click a label to change its name or color, then press <kbd>Enter</kbd> or click the check button.

You can also [update a label](https://resend.com/docs/api-reference/inboxes/update-label.md) via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.labels.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  labelId: '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
  name: 'Priority',
  color: '#F76B15',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->labels->update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
  [
    'name' => 'Priority',
    'color' => '#F76B15',
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Labels.UpdateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
  "name": "Priority",
  "color": "#F76B15",
}

resend.Inboxes.Labels.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "label_id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
  "name": "Priority",
  "color": "#F76B15",
}

Resend::Inboxes::Labels.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.UpdateInboxLabelRequest{
		Name:  "Priority",
		Color: "#F76B15",
	}

	client.Inboxes.Labels.Update(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
		params,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::UpdateInboxLabelOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let update = UpdateInboxLabelOptions::new()
    .with_name("Priority")
    .with_color("#F76B15");

  let _label = resend
    .inboxes
    .update_label(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
      update,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.UpdateInboxLabelOptions;
import com.resend.services.inboxes.model.UpdateInboxLabelResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxLabelOptions params = UpdateInboxLabelOptions.builder()
                .name("Priority")
                .color("#F76B15")
                .build();

        UpdateInboxLabelResponseSuccess data = resend.inboxes().labels().update(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxLabelUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" ),
    new InboxLabelUpdateData()
    {
        Name = "Priority",
        Color = "#F76B15",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/labels/7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "name": "Priority",
  "color": "#F76B15"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes labels update \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --label-id 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34 \
  --name Priority \
  --color '#F76B15'
```

## Delete a label

In the **Labels** tab of the inbox settings, click the trash icon next to the label. If the label is applied to any threads, you will be asked to confirm that you want to remove it from those threads.

Deleting a label removes it from every thread it was applied to. The threads themselves are not affected and stay in their current folders.

You can also [delete a label](https://resend.com/docs/api-reference/inboxes/delete-label.md) via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.labels.remove({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  labelId: '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->labels->remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Labels.remove(
  inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  label_id="7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "label_id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
}

Resend::Inboxes::Labels.remove(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Labels.Remove(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .inboxes
    .delete_label(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.RemoveInboxLabelResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveInboxLabelResponseSuccess data = resend.inboxes().labels().remove(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxLabelDeleteAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/labels/7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes labels delete \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --label-id 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34 \
  --yes
```

## API Reference

For complete API documentation, see the [Inbox Labels API reference](https://resend.com/docs/api-reference/inboxes/create-label.md).
