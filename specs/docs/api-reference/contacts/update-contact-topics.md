> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Contact Topics

> Update topic subscriptions for a contact.

## Path Parameters

Either `id` or `email` must be provided.

<ParamField path="id" type="string">
  The Contact ID.
</ParamField>

<ParamField path="email" type="string">
  The Contact Email.
</ParamField>

## Body Parameters

<ParamField body="topics" type="array" required>
  Array of topic subscription updates.

  <Expandable defaultOpen title="properties">
    <ParamField body="id" type="string" required>
      The Topic ID.
    </ParamField>

    <ParamField body="subscription" type="string" required>
      The subscription action. Must be either `opt_in` or `opt_out`.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  // Update by contact id
  const { data, error } = await resend.contacts.topics.update({
    id: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
    topics: [
      {
        id: 'b6d24b8e-af0b-4c3c-be0c-359bbd97381e',
        subscription: 'opt_out',
      },
      {
        id: '07d84122-7224-4881-9c31-1c048e204602',
        subscription: 'opt_in',
      },
    ],
  });

  // Update by contact email
  const { data, error } = await resend.contacts.topics.update({
    email: 'steve.wozniak@gmail.com',
    topics: [
      {
        id: '07d84122-7224-4881-9c31-1c048e204602',
        subscription: 'opt_out',
      },
      {
        id: '07d84122-7224-4881-9c31-1c048e204602',
        subscription: 'opt_in',
      },
    ],
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Update by contact id
  $resend->contacts->topics->update('e169aa45-1ecf-4183-9955-b1499d5701d3', [
    [
      'id' => '07d84122-7224-4881-9c31-1c048e204602',
      'subscription' => 'opt_out',
    ],
    [
      'id' => '07d84122-7224-4881-9c31-1c048e204602',
      'subscription' => 'opt_in',
    ],
  ]);

  // Update by contact email
  $resend->contacts->topics->update('steve.wozniak@gmail.com', [
    [
      'id' => '07d84122-7224-4881-9c31-1c048e204602',
      'subscription' => 'opt_out',
    ],
    [
      'id' => '07d84122-7224-4881-9c31-1c048e204602',
      'subscription' => 'opt_in',
    ],
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  # Update by contact id
  params = {
      "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
      "topics": [
          {"id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e", "subscription": "opt_out"},
          {"id": "07d84122-7224-4881-9c31-1c048e204602", "subscription": "opt_in"},
      ],
  }

  response = resend.Contacts.Topics.update(params)

  # Update by contact email
  params_by_email = {
      "email": "steve.wozniak@gmail.com",
      "topics": [
          {"id": "07d84122-7224-4881-9c31-1c048e204602", "subscription": "opt_out"},
          {"id": "07d84122-7224-4881-9c31-1c048e204602", "subscription": "opt_in"},
      ],
  }

  response = resend.Contacts.Topics.update(params_by_email)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Update by contact id
  update_params = {
    id: "e169aa45-1ecf-4183-9955-b1499d5701d3",
    topics: [
      { id: "b6d24b8e-af0b-4c3c-be0c-359bbd97381e", subscription: "opt_out" },
      { id: "07d84122-7224-4881-9c31-1c048e204602", subscription: "opt_in" }
    ]
  }
  updated_topics = Resend::Contacts::Topics.update(update_params)

  # Update by contact email
  update_params = {
    email: "steve.wozniak@gmail.com",
    topics: [
      { id: "07d84122-7224-4881-9c31-1c048e204602", subscription: "opt_out" },
      { id: "07d84122-7224-4881-9c31-1c048e204602", subscription: "opt_in" }
    ]
  }
  updated_topics = Resend::Contacts::Topics.update(update_params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	ctx := context.TODO()
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Update by contact id
  	params := &resend.UpdateContactTopicsRequest{
  		ContactId: "e169aa45-1ecf-4183-9955-b1499d5701d3",
  		Topics: []resend.TopicSubscriptionUpdate{
  			{
  				Id:           "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
  				Subscription: "opt_out",
  			},
  			{
  				Id:           "07d84122-7224-4881-9c31-1c048e204602",
  				Subscription: "opt_in",
  			},
  		},
  	}

  	updatedTopics, err := client.Contacts.Topics.UpdateWithContext(ctx, params)
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(updatedTopics)

  	// Update by contact email
  	params = &resend.UpdateContactTopicsRequest{
  		Email: "steve.wozniak@gmail.com",
  		Topics: []resend.TopicSubscriptionUpdate{
  			{
  				Id:           "07d84122-7224-4881-9c31-1c048e204602",
  				Subscription: "opt_out",
  			},
  			{
  				Id:           "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
  				Subscription: "opt_in",
  			},
  		},
  	}

  	updatedTopics, err = client.Contacts.Topics.UpdateWithContext(ctx, params)
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(updatedTopics)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    types::{SubscriptionType, UpdateContactTopicOptions},
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let topics = [
      UpdateContactTopicOptions::new(
        "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
        SubscriptionType::OptOut,
      ),
      UpdateContactTopicOptions::new(
        "07d84122-7224-4881-9c31-1c048e204602",
        SubscriptionType::OptIn,
      ),
    ];

    let _contact = resend
      .contacts
      .update_contact_topics("e169aa45-1ecf-4183-9955-b1499d5701d3", topics)
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
    public static void main(String[] args) {
      Resend resend = new Resend("re_xxxxxxxxx");

      // Update by contact id
      UpdateContactTopicsOptions optionsById = UpdateContactTopicsOptions.builder()
                  .id("e169aa45-1ecf-4183-9955-b1499d5701d3")
                  .topics(ContactTopicOptions.builder()
                              .id("b6d24b8e-af0b-4c3c-be0c-359bbd97381e")
                              .subscription("opt_out")
                              .build(),
                          ContactTopicOptions.builder()
                              .id("07d84122-7224-4881-9c31-1c048e204602")
                              .subscription("opt_in")
                              .build())
                  .build();

      resend.contacts().topics().update(optionsById);

      // Update by contact email
      UpdateContactTopicsOptions optionsByEmail = UpdateContactTopicsOptions.builder()
                  .email("steve.wozniak@gmail.com")
                  .topics(ContactTopicOptions.builder()
                              .id("07d84122-7224-4881-9c31-1c048e204602")
                              .subscription("opt_in")
                              .build(),
                          ContactTopicOptions.builder()
                              .id("b6d24b8e-af0b-4c3c-be0c-359bbd97381e")
                              .subscription("opt_out")
                              .build())
                  .build();

      resend.contacts().topics().update(optionsById);
    }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var topics = new List<TopicSubscription>();

  topics.Add( new TopicSubscription() {
    Id = new Guid( "07d84122-7224-4881-9c31-1c048e204602" ),
    Subscription = SubscriptionType.OptIn,
  });

  topics.Add( new TopicSubscription() {
    Id = new Guid( "b6d24b8e-af0b-4c3c-be0c-359bbd97381e" ),
    Subscription = SubscriptionType.OptOut,
  });

  await resend.ContactUpdateTopicsAsync(
      new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ),
      topics );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  // Update by contact id
  curl -X PATCH 'https://api.resend.com/contacts/e169aa45-1ecf-4183-9955-b1499d5701d3/topics' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'[
        {
          "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
          "subscription": "opt_out"
        }
       ]'

  // Update by contact email
  curl -X PATCH 'https://api.resend.com/contacts/steve.wozniak@gmail.com/topics' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'[
        {
          "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
          "subscription": "opt_out"
        }
       ]'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Update by contact id
  resend contacts update-topics e169aa45-1ecf-4183-9955-b1499d5701d3 \
    --topics '[{"id":"b6d24b8e-af0b-4c3c-be0c-359bbd97381e","subscription":"opt_out"}]'

  # Update by contact email
  resend contacts update-topics steve.wozniak@gmail.com \
    --topics '[{"id":"b6d24b8e-af0b-4c3c-be0c-359bbd97381e","subscription":"opt_out"}]'
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "contact_topics",
    "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e"
  }
  ```
</ResponseExample>
