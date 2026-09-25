> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Contact Topics

> Retrieve a list of topics subscriptions for a contact.

export const QueryParams = ({type, isRequired}) => {
  return <>
      <h2>Query Parameters</h2>

      {isRequired ? <ParamField query="limit" type="number">
          Number of {type} to retrieve.
          <ul>
            <li>
              Default value: <code>20</code>
            </li>
            <li>
              Maximum value: <code>100</code>
            </li>
            <li>
              Minimum value: <code>1</code>
            </li>
          </ul>
        </ParamField> : <>
          <p>
            Note that the <code>limit</code> parameter is <em>optional</em>. If
            you do not provide a <code>limit</code>, all {type} will be returned
            in a single response.
          </p>
          <ParamField query="limit" type="number">
            Number of {type} to retrieve.
            <ul>
              <li>
                Maximum value: <code>100</code>
              </li>
              <li>
                Minimum value: <code>1</code>
              </li>
            </ul>
          </ParamField>
        </>}

      <ParamField query="after" type="string">
        The ID <em>after</em> which we'll retrieve more {type} (for pagination).
        This ID will <em>not</em> be included in the returned list. Cannot be
        used with the
        <code>before</code> parameter.
      </ParamField>
      <ParamField query="before" type="string">
        The ID <em>before</em> which we'll retrieve more {type} (for
        pagination). This ID will <em>not</em> be included in the returned list.
        Cannot be used with the <code>after</code> parameter.
      </ParamField>
      <Info>
        You can only use either <code>after</code> or <code>before</code>{' '}
        parameter, not both. See our{' '}
        <a href="/docs/api-reference/pagination">pagination guide</a> for more
        information.
      </Info>
    </>;
};

## Path Parameters

Either `id` or `email` must be provided.

<ParamField path="id" type="string">
  The Contact ID.
</ParamField>

<ParamField path="email" type="string">
  The Contact Email.
</ParamField>

<QueryParams type="topics" isRequired={false} />

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.contacts.topics.list({
    id: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
    // or: email: 'steve.wozniak@gmail.com',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Get by contact id
  $resend->contacts->topics->get('e169aa45-1ecf-4183-9955-b1499d5701d3');

  // Get by contact email
  $resend->contacts->topics->get('steve.wozniak@gmail.com');
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  # Get by contact id
  topics = resend.Contacts.Topics.list(contact_id='e169aa45-1ecf-4183-9955-b1499d5701d3')

  # Get by contact email
  topics = resend.Contacts.Topics.list(email='steve.wozniak@gmail.com')
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Get by contact id
  contact_topics = Resend::Contacts::Topics.list(id: "e169aa45-1ecf-4183-9955-b1499d5701d3")

  # Get by contact email
  contact_topics = Resend::Contacts::Topics.list(email: "steve.wozniak@gmail.com")
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
  	ctx := context.TODO()
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Get by contact id
  	topics, err := client.Contacts.Topics.ListWithContext(ctx, "e169aa45-1ecf-4183-9955-b1499d5701d3")
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(topics)

  	// Get by contact email
  	topics, err = client.Contacts.Topics.ListWithContext(ctx, "steve.wozniak@gmail.com")
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(topics)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{list_opts::ListOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _topics = resend
      .contacts
      .get_contact_topics(
        "e169aa45-1ecf-4183-9955-b1499d5701d3",
        ListOptions::default(),
      )
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;

  public class Main {
    public static void main(String[] args) throws ResendException {
      Resend resend = new Resend("re_xxxxxxxxx");

      // Get by contact id
      resend.contacts().topics().list("e169aa45-1ecf-4183-9955-b1499d5701d3");

      // Get by contact email
      resend.contacts().topics().list("steve.wozniak@gmail.com");
    }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.ContactListTopicsAsync( new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ));
  Console.WriteLine( "Nr Topics={0}", resp.Content.Data.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  // Get by contact id
  curl -X GET 'https://api.resend.com/contacts/e169aa45-1ecf-4183-9955-b1499d5701d3/topics' \
       -H 'Authorization: Bearer re_xxxxxxxxx'

  // Get by contact email
  curl -X GET 'https://api.resend.com/contacts/steve.wozniak@gmail.com/topics' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Get by contact id
  resend contacts topics e169aa45-1ecf-4183-9955-b1499d5701d3

  # Get by contact email
  resend contacts topics steve.wozniak@gmail.com
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
        "name": "Product Updates",
        "description": "New features, and latest announcements.",
        "subscription": "opt_in"
      }
    ]
  }
  ```
</ResponseExample>
