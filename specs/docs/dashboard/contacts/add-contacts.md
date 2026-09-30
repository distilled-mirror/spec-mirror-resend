> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Add Contacts

> Learn how to add Contacts with Resend.

## Add Contacts

You can add a Contact in several different ways:

* [CSV upload](#add-contacts-by-uploading-a-csv)
* [API](#add-contacts-programmatically-via-api)
* [CLI](/docs/cli#contacts)
* [manually in the Dashboard](#add-contacts-manually)

<Note>
  Contacts are also created automatically when an
  [Automation](/docs/dashboard/automations/introduction) runs for an email address
  that doesn't yet exist in your Contact list.
</Note>

### Add Contacts programmatically via API

When you create Contacts programmatically using the [Contacts API](/docs/api-reference/contacts/create-contact), an email address is the only required property. You can optionally pass [Contact properties available by default](/docs/dashboard/contacts/properties#included-properties), or any [custom Contact properties](/docs/dashboard/contacts/properties#add-custom-contact-properties) you have previously defined.

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  resend.contacts.create({
    email: 'steve.wozniak@gmail.com',
    firstName: 'Steve',
    lastName: 'Wozniak',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->contacts->create(
    parameters: [
      'email' => 'steve.wozniak@gmail.com',
      'first_name' => 'Steve',
      'last_name' => 'Wozniak',
    ]
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Contacts.CreateParams = {
    "email": "steve.wozniak@gmail.com",
    "first_name": "Steve",
    "last_name": "Wozniak",
  }

  resend.Contacts.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    "email": "steve.wozniak@gmail.com",
    "first_name": "Steve",
    "last_name": "Wozniak",
  }

  Resend::Contacts.create(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.CreateContactRequest{
  		Email:        "steve.wozniak@gmail.com",
  		FirstName:    "Steve",
  		LastName:     "Wozniak",
  		Unsubscribed: false,
  	}

  	client.Contacts.Create(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::CreateContactOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let contact = CreateContactOptions::new("steve.wozniak@gmail.com")
      .with_first_name("Steve")
      .with_last_name("Wozniak");

    let _contact = resend
      .contacts
      .create(contact)
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.contacts.model.CreateContactOptions;
  import com.resend.services.contacts.model.CreateContactResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateContactOptions params = CreateContactOptions.builder()
                  .email("steve.wozniak@gmail.com")
                  .firstName("Steve")
                  .lastName("Wozniak")
                  .build();

          CreateContactResponseSuccess data = resend.contacts().create(params);
      }
  }
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/contacts' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "email": "steve.wozniak@gmail.com",
    "first_name": "Steve",
    "last_name": "Wozniak"
  }'
  ```
</CodeGroup>

Once a Contact is created, you can update it using the [update Contact](/docs/api-reference/contacts/update-contact) endpoint. There are also endpoints to [add the Contact to a Segment](/docs/api-reference/contacts/add-contact-to-segment) and to [update Topics for a Contact](/docs/api-reference/contacts/update-contact-topics).

### Add Contacts by uploading a .csv

If you already have a list of existing email addresses, you can add multiple Contacts at once by uploading a .csv file on the [Dashboard page](https://resend.com/audience).

<Steps>
  <Step title="Go to the Dashboard page and select **Add contacts**." />

  <Step title="Select **Import CSV**." />

  <Step title="Upload your CSV file from your computer." />

  <Step title="Map the fields you want to use.">
    You can map the fields to the [included Contact
    properties](/docs/dashboard/contacts/properties#included-properties) such as
    `email` and `first_name`, or any [custom Contact
    properties](/docs/dashboard/contacts/properties#add-custom-contact-properties)
    you've already created.
  </Step>

  <Step title="Optionally add the Contacts to an existing Segment.">
    Broadcasts are usually sent to a Segment of your Contact list. Add a Segment
    to determine which marketing emails you will send to the Contacts.
  </Step>

  <Step title="Optionally add the Contacts to an existing Topic.">
    You can subscribe your Contacts to one or more Broadcast Topics. They will
    have the option to unsubscribe from your unsubscribe page.
  </Step>

  <Step title="Select **Continue**, review the Contacts, and finish the upload." />
</Steps>

### Add Contacts manually

<Steps>
  <Step title="Navigate to the Dashboard page." />

  <Step title="Select **Add contacts**." />

  <Step title="Select **Add Manually** from the dropdown." />

  <Step title="Add the email address of the Contact in the text field (separated by commas or new lines for multiple Contacts)." />

  <Step title="Optionally add the new Contact to one or more existing Segments.">
    <Info>
      An email address is the only required property for a new Contact. However,
      in most cases, a Contact must belong to a Segment in order to receive a
      Broadcast.
    </Info>
  </Step>

  <Step title="Optionally add the new Contact to one or more existing Topics." />

  <Step title="Confirm and click **Add**." />
</Steps>

## API Reference

For complete API documentation, see the [Contacts API reference](/docs/api-reference/contacts/create-contact).
