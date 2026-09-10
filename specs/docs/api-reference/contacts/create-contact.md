> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Contact

> Create a contact.

export const ResendParamField = ({children, body, path, ...props}) => {
  const [lang, setLang] = useState(() => {
    return localStorage.getItem('code') || '"Node.js"';
  });
  useEffect(() => {
    const onStorage = event => {
      const key = event.detail.key;
      if (key === 'code') {
        setLang(event.detail.value);
      }
    };
    document.addEventListener('mintlify-localstorage', onStorage);
    return () => {
      document.removeEventListener('mintlify-localstorage', onStorage);
    };
  }, []);
  const toCamelCase = str => typeof str === 'string' ? str.replace(/[_-](\w)/g, (_, c) => c.toUpperCase()) : str;
  const resolvedBody = useMemo(() => {
    const value = JSON.parse(lang);
    return value === 'Node.js' ? toCamelCase(body) : body;
  }, [body, lang]);
  const resolvedPath = useMemo(() => {
    const value = JSON.parse(lang);
    return value === 'Node.js' ? toCamelCase(path) : path;
  }, [path, lang]);
  return <ParamField body={resolvedBody} path={resolvedPath} {...props}>
      {children}
    </ParamField>;
};

## Body Parameters

<ParamField body="email" type="string" required>
  The email address of the contact.
</ParamField>

<ResendParamField body="first_name" type="string">
  The first name of the contact.
</ResendParamField>

<ResendParamField body="last_name" type="string">
  The last name of the contact.
</ResendParamField>

<ParamField body="unsubscribed" type="boolean">
  The Contact's global subscription status. If set to `true`, the contact will
  be unsubscribed from all Broadcasts.
</ParamField>

<ParamField body="properties" type="object">
  A map of custom property keys and values to create.

  <Expandable defaultOpen title="custom properties">
    <ParamField body="key" type="string" required>
      The property key.
    </ParamField>

    <ParamField body="value" type="string" required>
      The property value.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="segments" type="array">
  Array of objects. Each object must contain the ID of the segment that you'd like to add the contact to.

  <Expandable defaultOpen title="segments">
    <ParamField body="id" type="string" required>
      The segment ID.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="topics" type="array">
  Array of topic subscriptions for the contact.

  <Expandable defaultOpen title="topics">
    <ParamField body="id" type="string" required>
      The topic ID.
    </ParamField>

    <ParamField body="subscription" type="'opt_in' | 'opt_out'" required>
      The subscription status for this topic.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.contacts.create({
    email: 'steve.wozniak@gmail.com',
    firstName: 'Steve',
    lastName: 'Wozniak',
    unsubscribed: false,
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->contacts->create(
    parameters: [
      'email' => 'steve.wozniak@gmail.com',
      'first_name' => 'Steve',
      'last_name' => 'Wozniak',
      'unsubscribed' => false
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
    "unsubscribed": False,
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
    "unsubscribed": false,
  }

  Resend::Contacts.create(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

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
      .with_last_name("Wozniak")
      .with_unsubscribed(false);

    let _contact = resend.contacts.create(contact).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateContactOptions params = CreateContactOptions.builder()
                  .email("steve.wozniak@gmail.com")
                  .firstName("Steve")
                  .lastName("Wozniak")
                  .unsubscribed(false)
                  .build();

          CreateContactResponseSuccess data = resend.contacts().create(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.ContactAddAsync(
      new ContactData()
      {
          Email = "steve.wozniak@gmail.com",
          FirstName = "Steve",
          LastName = "Wozniak",
          IsUnsubscribed = false,
      }
  );
  Console.WriteLine( "Contact Id={0}", resp.Content );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/contacts' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "email": "steve.wozniak@gmail.com",
    "first_name": "Steve",
    "last_name": "Wozniak",
    "unsubscribed": false
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend contacts create \
    --email steve.wozniak@gmail.com \
    --first-name Steve \
    --last-name Wozniak
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "contact",
    "id": "479e3145-dd38-476b-932c-529ceb705947"
  }
  ```
</ResponseExample>
