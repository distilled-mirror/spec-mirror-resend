> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Automation Run

> Retrieve a single automation run.

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

<ResendParamField path="automation_id" type="string" required>
  The automation ID.
</ResendParamField>

<ResendParamField path="run_id" type="string" required>
  The automation run ID.
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.automations.runs.get({
    automationId: 'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
    runId: 'a1b2c3d4-e5f6-7890-abcd-ef1234567890',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->automations->runs->get(
    'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
    'a1b2c3d4-e5f6-7890-abcd-ef1234567890',
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Automations.Runs.get(
    "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
    "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Automations::Runs.get(
    "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
    "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Automations.GetRun(
  		"c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
  		"a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  	)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _automation = resend
      .automations
      .get_run(
        "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
        "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
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

          AutomationRun data = resend.automations().getRun(
                  GetAutomationRunOptions.builder()
                          .automationId("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
                          .runId("a1b2c3d4-e5f6-7890-abcd-ef1234567890")
                          .build()
          );
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  var resp = await resend.AutomationRunRetrieveAsync(
      new Guid( "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd" ),
      new Guid( "a1b2c3d4-e5f6-7890-abcd-ef1234567890" )
  );
  Console.WriteLine( "Status={0}", resp.Content.Status );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/automations/c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd/runs/a1b2c3d4-e5f6-7890-abcd-ef1234567890' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend automations runs get --automation-id c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd --run-id a1b2c3d4-e5f6-7890-abcd-ef1234567890
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "automation_run",
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "status": "completed",
    "started_at": "2026-10-01 12:00:00.000000+00",
    "completed_at": "2026-10-01 12:05:00.000000+00",
    "created_at": "2026-10-01 12:00:00.000000+00",
    "steps": [
      {
        "key": "start",
        "type": "trigger",
        "status": "completed",
        "started_at": "2026-10-01 12:00:00.000000+00",
        "completed_at": "2026-10-01 12:00:01.000000+00",
        "output": null,
        "error": null,
        "created_at": "2026-10-01 12:00:00.000000+00"
      },
      {
        "key": "welcome",
        "type": "send_email",
        "status": "completed",
        "started_at": "2026-10-01 12:00:01.000000+00",
        "completed_at": "2026-10-01 12:00:02.000000+00",
        "output": null,
        "error": null,
        "created_at": "2026-10-01 12:00:01.000000+00"
      }
    ]
  }
  ```
</ResponseExample>
