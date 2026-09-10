> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Contact Import

> Create a contact import.

## Body Parameters

This endpoint accepts `multipart/form-data`. Object and array fields
(`column_map`, `segments`, `topics`) must be sent as JSON-encoded strings.

<ParamField body="file" type="file" required>
  The CSV file to import. The file must be sent as a form field named `file`.
  Maximum file size is 200MB.
</ParamField>

<ParamField body="column_map" type="object">
  Maps CSV columns to contact fields.

  <Expandable defaultOpen title="column_map">
    <ParamField body="email" type="string">
      The CSV column that contains contact email addresses.
    </ParamField>

    <ParamField body="first_name" type="string">
      The CSV column that contains contact first names.
    </ParamField>

    <ParamField body="last_name" type="string">
      The CSV column that contains contact last names.
    </ParamField>

    <ParamField body="unsubscribed" type="string">
      The CSV column that contains the contact's global subscription status.
    </ParamField>

    <ParamField body="properties" type="object">
      A map of custom property keys to CSV columns.

      <Expandable title="properties">
        <ParamField body="key" type="object">
          The custom property key.

          <Expandable title="property mapping">
            <ParamField body="column" type="string" required>
              The CSV column that contains the custom property value.
            </ParamField>

            <ParamField body="type" type="'string' | 'number' | 'boolean'">
              The custom property value type. Defaults to `string`.
            </ParamField>
          </Expandable>
        </ParamField>
      </Expandable>
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="on_conflict" type="'upsert' | 'skip'">
  How to handle contacts that already exist. Defaults to `upsert`.
</ParamField>

<ParamField body="segments" type="array">
  Array of objects. Each object must contain the ID of the segment that you'd
  like to add the imported contacts to.

  <Expandable defaultOpen title="segments">
    <ParamField body="id" type="string" required>
      The segment UUID.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="topics" type="array">
  Array of topic subscriptions for imported contacts.

  <Expandable defaultOpen title="topics">
    <ParamField body="id" type="string" required>
      The Topic UUID.
    </ParamField>

    <ParamField body="subscription" type="'opt_in' | 'opt_out'" required>
      The subscription status for this topic.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { readFile } from 'node:fs/promises';
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const file = new Blob([await readFile('contacts.csv')], {
    type: 'text/csv',
  });

  const { data, error } = await resend.contacts.imports.create({
    file,
    columnMap: {
      email: 'Email',
      firstName: 'First Name',
      lastName: 'Last Name',
      properties: {
        plan: {
          column: 'Plan',
          type: 'string',
        },
      },
    },
    onConflict: 'upsert',
    segments: [{ id: '78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6' }],
    topics: [
      {
        id: '059ac693-2fc8-4c13-8b27-01350d638a17',
        subscription: 'opt_in',
      },
    ],
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $file = fopen('contacts.csv', 'r');

  $resend->contacts->imports->create([
    'file' => $file,
    'column_map' => [
      'email' => 'Email',
      'first_name' => 'First Name',
      'last_name' => 'Last Name',
      'properties' => [
        'plan' => [
          'column' => 'Plan',
          'type' => 'string',
        ],
      ],
    ],
    'on_conflict' => 'upsert',
    'segments' => [['id' => '78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6']],
    'topics' => [
      [
        'id' => '059ac693-2fc8-4c13-8b27-01350d638a17',
        'subscription' => 'opt_in',
      ],
    ],
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  with open("contacts.csv", "rb") as f:
      file_content = f.read()

  params: resend.Contacts.Imports.CreateParams = {
      "file": file_content,
      "column_map": {
          "email": "Email",
          "first_name": "First Name",
          "last_name": "Last Name",
          "properties": {
              "plan": {
                  "column": "Plan",
                  "type": "string",
              },
          },
      },
      "on_conflict": "upsert",
      "segments": [{"id": "78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6"}],
      "topics": [
          {
              "id": "059ac693-2fc8-4c13-8b27-01350d638a17",
              "subscription": "opt_in",
          },
      ],
  }

  resend.Contacts.Imports.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    file: File.read("contacts.csv"),
    column_map: {
      "email" => "Email",
      "first_name" => "First Name",
      "last_name" => "Last Name",
      "properties" => {
        "plan" => {
          "column" => "Plan",
          "type" => "string"
        }
      }
    },
    on_conflict: "upsert",
    segments: [{ id: "78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6" }],
    topics: [
      { id: "059ac693-2fc8-4c13-8b27-01350d638a17", subscription: "opt_in" }
    ]
  }

  Resend::Contacts::Imports.create(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"os"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	file, err := os.ReadFile("contacts.csv")
  	if err != nil {
  		panic(err)
  	}

  	params := &resend.CreateContactImportRequest{
  		File:       file,
  		Filename:   "contacts.csv",
  		OnConflict: "upsert",
  		ColumnMap: map[string]any{
  			"email":      "Email",
  			"first_name": "First Name",
  			"last_name":  "Last Name",
  			"properties": map[string]any{
  				"plan": map[string]any{
  					"column": "Plan",
  					"type":   "string",
  				},
  			},
  		},
  		Segments: []resend.ContactImportSegment{{Id: "78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6"}},
  		Topics: []resend.TopicSubscriptionUpdate{
  			{Id: "059ac693-2fc8-4c13-8b27-01350d638a17", Subscription: "opt_in"},
  		},
  	}

  	client.Contacts.Imports.Create(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use std::fs::File;

  use resend_rs::{
    Resend, Result,
    types::{
      ContactImportColumnMap, ContactImportOnConflict, ContactImportPropertyMapping,
      ContactImportPropertyType, ContactImportTopic, ContactImportTopicSubscription,
      CreateContactImportOptions,
    },
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let file = File::open("contacts.csv").unwrap();

    let contact_import = CreateContactImportOptions::new()
      .with_column_map(
        ContactImportColumnMap::new()
          .with_email("Email")
          .with_first_name("First Name")
          .with_last_name("Last Name")
          .with_property(
            "plan",
            ContactImportPropertyMapping {
              column: "Plan".to_owned(),
              r#type: ContactImportPropertyType::String,
            },
          ),
      )
      .with_on_conflict(ContactImportOnConflict::Upsert)
      .with_segment("78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6")
      .with_topic(ContactImportTopic {
        id: "059ac693-2fc8-4c13-8b27-01350d638a17".to_owned(),
        subscription: ContactImportTopicSubscription::OptIn,
      });

    let _data = resend.contacts.create_import(file, contact_import).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.services.contacts.model.*;
  import java.io.File;

  public class Main {
      public static void main(String[] args) throws Exception {
          Resend resend = new Resend("re_xxxxxxxxx");

          ContactImportColumnMap columnMap = ContactImportColumnMap.builder()
                  .email("Email")
                  .firstName("First Name")
                  .lastName("Last Name")
                  .property("plan", ContactImportPropertyMapping.builder()
                          .column("Plan")
                          .type("string")
                          .build())
                  .build();

          CreateContactImportOptions params = CreateContactImportOptions.builder()
                  .file(new File("contacts.csv"))
                  .columnMap(columnMap)
                  .onConflict("upsert")
                  .segments(new ContactImportSegmentReference("78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6"))
                  .topics(ContactImportTopicSubscription.builder()
                          .id("059ac693-2fc8-4c13-8b27-01350d638a17")
                          .subscription("opt_in")
                          .build())
                  .build();

          CreateContactImportResponseSuccess data = resend.contacts().imports().create(params);
      }
  }
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/contacts/imports' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -F 'file=@contacts.csv;type=text/csv' \
       -F 'column_map={"email":"Email","first_name":"First Name","last_name":"Last Name","properties":{"plan":{"column":"Plan","type":"string"}}}' \
       -F 'on_conflict=upsert' \
       -F 'segments=[{"id":"78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6"}]' \
       -F 'topics=[{"id":"059ac693-2fc8-4c13-8b27-01350d638a17","subscription":"opt_in"}]'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend contacts imports create \
    --file contacts.csv \
    --column-map '{"email":"Email","firstName":"First Name","lastName":"Last Name","properties":{"plan":{"column":"Plan","type":"string"}}}' \
    --on-conflict upsert \
    --segment-id 78e7a5c6-9a91-4c63-9d1f-3b9c0b5b9ab6 \
    --topics '[{"id":"059ac693-2fc8-4c13-8b27-01350d638a17","subscription":"opt_in"}]'
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "contact_import",
    "id": "479e3145-dd38-476b-932c-529ceb705947"
  }
  ```
</ResponseExample>
