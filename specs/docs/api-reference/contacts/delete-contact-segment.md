> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Contact Segment

> Remove an existing contact from a segment.

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

## Path Parameters

Either `id` or `email` must be provided.

<ParamField path="id" type="string">
  The Contact ID.
</ParamField>

<ParamField path="email" type="string">
  The Contact Email.
</ParamField>

<ResendParamField path="segment_id" type="string" required>
  The Segment ID.
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  // Remove by contact id
  const { data, error } = await resend.contacts.segments.remove({
    contactId: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
  });

  // Remove by contact email
  const { data, error } = await resend.contacts.segments.remove({
    email: 'steve.wozniak@gmail.com',
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Remove by contact id
  $resend->contacts->segments->remove(
    contact: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf'
  );

  // Remove by contact email
  $resend->contacts->segments->remove(
    contact: 'steve.wozniak@gmail.com',
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  # Remove by contact id
  params = {
      "segment_id": '78261eea-8f8b-4381-83c6-79fa7120f1cf',
      "contact_id": 'e169aa45-1ecf-4183-9955-b1499d5701d3',
  }

  response = resend.Contacts.Segments.remove(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require 'resend'

  Resend.api_key = 're_xxxxxxxxx'

  # Remove by contact id
  removed = Resend::Contacts::Segments.remove(
    contact_id: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
    segment_id: '78261eea-8f8b-4381-83c6-79fa7120f1cf'
  )

  # Remove by contact email
  removed = Resend::Contacts::Segments.remove(
    email: 'steve.wozniak@gmail.com',
    segment_id: '78261eea-8f8b-4381-83c6-79fa7120f1cf'
  )
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

  	// Remove by contact id
  	removeParams := &resend.RemoveContactSegmentRequest{
  		ContactId: "e169aa45-1ecf-4183-9955-b1499d5701d3",
  		SegmentId: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
  	}

  	response, err := client.Contacts.Segments.RemoveWithContext(ctx, removeParams)
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(response)

  	// Remove by contact email
  	removeByEmailParams := &resend.RemoveContactSegmentRequest{
  		Email:     "steve.wozniak@gmail.com",
  		SegmentId: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
  	}

  	response, err = client.Contacts.Segments.RemoveWithContext(ctx, removeByEmailParams)
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(response)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    // Remove by contact id
    let _contact = resend
      .contacts
      .delete_contact_segment(
        "e169aa45-1ecf-4183-9955-b1499d5701d3",
        "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      )
      .await?;

    // Remove by contact email
    let _contact = resend
      .contacts
      .delete_contact_segment(
        "steve.wozniak@gmail.com",
        "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      )
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
    public static void main(String[] args) {
      Resend resend = new Resend("re_xxxxxxxxx");

      // Remove by contact id
      RemoveContactFromSegmentOptions optionsById = RemoveContactFromSegmentOptions.builder()
        .id("e169aa45-1ecf-4183-9955-b1499d5701d3")
        .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
        .build();

      resend.contacts().segments().remove(optionsById);

      // Remove by contact email
      RemoveContactFromSegmentOptions optionsByEmail = RemoveContactFromSegmentOptions.builder()
        .email("steve.wozniak@gmail.com")
        .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
        .build();

      resend.contacts().segments().remove(optionsByEmail);
    }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  await resend.ContactRemoveFromSegmentAsync(
      contactId: new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ),
      segmentId: new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" )
  );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Remove by contact id
  curl -X DELETE 'https://api.resend.com/contacts/e169aa45-1ecf-4183-9955-b1499d5701d3/segments/78261eea-8f8b-4381-83c6-79fa7120f1cf' \
       -H 'Authorization: Bearer re_xxxxxxxxx'

  # Remove by contact email
  curl -X DELETE 'https://api.resend.com/contacts/steve.wozniak@gmail.com/segments/78261eea-8f8b-4381-83c6-79fa7120f1cf' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Remove by contact id
  resend contacts remove-segment e169aa45-1ecf-4183-9955-b1499d5701d3 78261eea-8f8b-4381-83c6-79fa7120f1cf

  # Remove by contact email
  resend contacts remove-segment steve.wozniak@gmail.com 78261eea-8f8b-4381-83c6-79fa7120f1cf
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "contact_segment",
    "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
    "audienceId": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "deleted": true
  }
  ```
</ResponseExample>
