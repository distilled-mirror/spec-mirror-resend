> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Share Email

> Create a shareable link to view a sent or received email.

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

<ResendParamField path="id" type="string" required>
  The Email ID.
</ResendParamField>

## Body Parameters

<ResendParamField body="expires_in" type="string" default="48h">
  How long the link stays valid for, as a duration like `10m`, `2 hours`, or `1
      day`. Defaults to `48h` and cannot exceed 48 hours.
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.emails.share(
    '49a3999c-0ce1-4ea6-ab68-afcd6dc2e794',
    { expiresIn: '2 hours' },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->share('49a3999c-0ce1-4ea6-ab68-afcd6dc2e794', [
    'expires_in' => '2 hours'
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  share_params: resend.Emails.ShareParams = {
    "expires_in": "2 hours"
  }

  resend.Emails.share(
    email_id="49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
    params=share_params
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Emails.share(
    "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
    expires_in: "2 hours"
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"fmt"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	shareParams := &resend.ShareEmailRequest{
  		ExpiresIn: "2 hours",
  	}

  	shared, err := client.Emails.Share("49a3999c-0ce1-4ea6-ab68-afcd6dc2e794", shareParams)
  	if err != nil {
  		panic(err)
  	}
  	fmt.Println(shared.Url)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::ShareEmailOptions;
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let share = ShareEmailOptions::new()
      .with_expires_in("2 hours");

    let _shared = resend
      .emails
      .share("49a3999c-0ce1-4ea6-ab68-afcd6dc2e794", share)
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.ShareEmailOptions;
  import com.resend.services.emails.model.ShareEmailResponse;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          ShareEmailOptions shareParams = ShareEmailOptions.builder()
                  .expiresIn("2 hours")
                  .build();

          ShareEmailResponse data = resend
            .emails()
            .share("49a3999c-0ce1-4ea6-ab68-afcd6dc2e794", shareParams);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  await resend.EmailShareAsync(
      new Guid( "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794" ),
      "2 hours" );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails/49a3999c-0ce1-4ea6-ab68-afcd6dc2e794/share' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "expires_in": "2 hours"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails share 49a3999c-0ce1-4ea6-ab68-afcd6dc2e794 \
    --expires-in "2 hours"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "email",
    "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
    "url": "https://resend.com/shared?token=eyJhbGciOiJIUzI1NiJ9..."
  }
  ```
</ResponseExample>
