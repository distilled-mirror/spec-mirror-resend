> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update API key

> Update the name of an existing API key.

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

<Info>
  This endpoint only updates the API key's name. To change an API key's
  [permission or domain](/docs/dashboard/api-keys/introduction#edit-api-key-details),
  edit the key in the [Resend Dashboard](https://resend.com/api-keys).
</Info>

## Path Parameters

<ResendParamField path="api_key_id" type="string" required>
  The API key ID.
</ResendParamField>

## Body Parameters

<ParamField body="name" type="string" required>
  The API key name. Maximum 50 characters.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.apiKeys.update(
    'b6d24b8e-af0b-4c3c-be0c-359bbd97381e',
    { name: 'Production' },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->apiKeys->update('b6d24b8e-af0b-4c3c-be0c-359bbd97381e', [
    'name' => 'Production'
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.ApiKeys.UpdateParams = {
    "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
    "name": "Production",
  }

  resend.ApiKeys.update(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    id: "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
    name: "Production"
  }
  Resend::ApiKeys.update(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")
  	params := &resend.UpdateApiKeyRequest{
  		Name: "Production",
  	}
  	client.ApiKeys.Update("b6d24b8e-af0b-4c3c-be0c-359bbd97381e", params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::UpdateApiKeyOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _api_key = resend
      .api_keys
      .update(
        "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
        UpdateApiKeyOptions::new("Production"),
      )
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.apikeys.model.UpdateApiKeyOptions;
  import com.resend.services.apikeys.model.UpdateApiKeyResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          UpdateApiKeyOptions params = UpdateApiKeyOptions
                  .builder()
                  .name("Production").build();

          UpdateApiKeyResponseSuccess apiKey = resend.apiKeys().update("b6d24b8e-af0b-4c3c-be0c-359bbd97381e", params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.ApiKeyUpdateAsync( new Guid( "b6d24b8e-af0b-4c3c-be0c-359bbd97381e" ), "Production" );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X PATCH 'https://api.resend.com/api-keys/b6d24b8e-af0b-4c3c-be0c-359bbd97381e' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "Production"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend api-keys update b6d24b8e-af0b-4c3c-be0c-359bbd97381e --name Production
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "api_key",
    "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e"
  }
  ```
</ResponseExample>
