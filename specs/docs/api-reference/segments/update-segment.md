> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Segment

> Update an existing segment.

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

<ResendParamField path="segment_id" type="string" required>
  The Segment ID.
</ResendParamField>

## Body Parameters

<ParamField body="name" type="string" required>
  The name of the segment.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.segments.update(
    '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    {
      name: 'Active Users',
    },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->segments->update('78261eea-8f8b-4381-83c6-79fa7120f1cf', [
    'name' => 'Active Users',
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  params: resend.Segments.UpdateParams = {
      "name": "Active Users",
  }

  segment = resend.Segments.update('78261eea-8f8b-4381-83c6-79fa7120f1cf', params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    segment_id: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    name: "Active Users"
  }
  Resend::Segments.update(params)
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

  	params := &resend.UpdateSegmentRequest{
  		Name: "Active Users",
  	}

  	segment, err := client.Segments.UpdateWithContext(ctx, "78261eea-8f8b-4381-83c6-79fa7120f1cf", params)
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(segment)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _segment = resend
      .segments
      .update("78261eea-8f8b-4381-83c6-79fa7120f1cf", "Active Users")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          UpdateSegmentOptions options = UpdateSegmentOptions.builder()
              .name("Active Users")
              .build();

          UpdateSegmentResponseSuccess response = resend.segments().update("78261eea-8f8b-4381-83c6-79fa7120f1cf", options);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.SegmentUpdateAsync( new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ), new SegmentData() {
    Name = "Active Users",
  } );
  Console.WriteLine( "Segment Id={0}", resp.Content.Id );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X PATCH 'https://api.resend.com/segments/78261eea-8f8b-4381-83c6-79fa7120f1cf' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "Active Users"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend segments update 78261eea-8f8b-4381-83c6-79fa7120f1cf --name "Active Users"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "segment",
    "id": "78261eea-8f8b-4381-83c6-79fa7120f1cf"
  }
  ```
</ResponseExample>
