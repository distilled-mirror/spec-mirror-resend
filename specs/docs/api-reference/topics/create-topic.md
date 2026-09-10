> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Topic

> Create and email topics to segment your audience.

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

<ParamField body="name" type="string" required>
  The topic name. Max length is `50` characters.
</ParamField>

<ResendParamField body="default_subscription" type="string" required>
  The default subscription preference for new contacts. Possible values:
  `opt_in` or `opt_out`.

  <Note>
    This value cannot be changed later.
  </Note>
</ResendParamField>

<ParamField body="description" type="string">
  The topic description. Max length is `200` characters.
</ParamField>

<ResendParamField body="visibility" type="string">
  The visibility of the topic on the unsubscribe page. Possible values: `public` or `private`.

  * `private`: only contacts who are opted in to the topic can see it on the unsubscribe page.
  * `public`: all contacts can see the topic on the unsubscribe page.

  If not specified, defaults to `private`.
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.topics.create({
    name: 'Weekly Newsletter',
    defaultSubscription: 'opt_in',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->topics->create([
    'name' => 'Weekly Newsletter',
    'default_subscription' => 'opt_in',
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Topics.create({
      "name": "Weekly Newsletter",
      "default_subscription": "opt_in",
      "description": "Subscribe to our weekly newsletter for updates",
  })
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Topics.create(
    name: "Weekly Newsletter",
    default_subscription: "opt_in"
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  import (
  	"context"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Topics.CreateWithContext(context.TODO(), &resend.CreateTopicRequest{
  		Name:                "Weekly Newsletter",
  		DefaultSubscription: resend.DefaultSubscriptionOptIn,
  	})
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    types::{CreateTopicOptions, SubscriptionType},
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let opts = CreateTopicOptions::new("Weekly Newsletter", SubscriptionType::OptIn);
    let _topic = resend.topics.create(opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
    public static void main(String[] args) {
      Resend resend = new Resend("re_xxxxxxxxx");

      CreateTopicOptions createTopicOptions = CreateTopicOptions.builder()
        .name("Weekly Newsletter")
        .defaultSubscription("opt_in")
        .build();

      CreateTopicResponseSuccess response = resend.topics().create(createTopicOptions);
    }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.TopicCreateAsync( new TopicData() {
    Name = "Weekly Newsletter",
    Description = "Weekly newsletter for our subscribers",
    SubscriptionDefault = SubscriptionType.OptIn,
  } );
  Console.WriteLine( "Topic Id={0}", resp.Content );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/topics' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "Weekly Newsletter",
    "default_subscription": "opt_in"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend topics create --name "Weekly Newsletter" --default-subscription opt_in
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "topic",
    "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e"
  }
  ```
</ResponseExample>
