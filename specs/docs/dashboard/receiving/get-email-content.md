> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Email Content

> Get the body and headers of a received email.

Receiving emails contain the HTML and Plain Text body of the email, as well as the headers.

<Info>
  Webhooks do not include the email body, headers, or attachments, only their
  metadata. You must call the [Received emails
  API](/docs/api-reference/emails/retrieve-received-email) or the [Attachments
  API](/docs/api-reference/emails/list-received-email-attachments) to retrieve them.
  This design choice supports large attachments in serverless environments that
  have limited request body sizes.
</Info>

After receiving the webhook event, call the [Receiving API](/docs/api-reference/emails/retrieve-received-email).

Here are some examples:

<CodeGroup>
  ```ts Next.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  // app/api/events/route.ts
  import type { NextRequest } from 'next/server';
  import { NextResponse } from 'next/server';
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  export const POST = async (request: NextRequest) => {
    const event = await request.json();

    if (event.type === 'email.received') {
      const { data: email } = await resend.emails.receiving.get(
        event.data.email_id,
      );

      if (!email) {
        return NextResponse.json({ error: 'Email not found' }, { status: 404 });
      }

      console.log(email.html);
      console.log(email.text);
      console.log(email.headers);

      return NextResponse.json(email);
    }

    return NextResponse.json({});
  };
  ```

  ```php Laravel theme={"theme":{"light":"github-light","dark":"vesper"}}
  // routes/api.php
  use Illuminate\Http\JsonResponse;
  use Illuminate\Http\Request;
  use Illuminate\Support\Facades\Log;
  use Illuminate\Support\Facades\Route;
  use Resend\Laravel\Facades\Resend;

  Route::post('/events', function (Request $request) {
      $event = $request->json()->all();

      if ($event['type'] === 'email.received') {
          $email = Resend::emails()->receiving->get($event['data']['email_id']);

          Log::info($email->html);
          Log::info($email->text);
          Log::info(print_r($email->headers, true));

          return new JsonResponse($email);
      }

      return new JsonResponse([]);
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  // index.php
  // Include Composer autoload file to load Resend SDK classes...
  require __DIR__ . '/vendor/autoload.php';

  header('Content-Type: application/json');

  if ($_SERVER['REQUEST_METHOD'] !== 'POST') {
      http_response_code(405);
      echo json_encode(['error' => 'Method Not Allowed']);
      exit;
  }

  $body = file_get_contents('php://input');
  $event = json_decode($body, true);

  if (json_last_error() !== JSON_ERROR_NONE) {
      http_response_code(400);
      echo json_encode(['error' => 'Invalid JSON']);
      exit;
  }

  if ($event['type'] === 'email.received') {
      $resend = Resend::client('re_xxxxxxxxx');

      $email = $resend->emails->receiving->get($event['data']['email_id']);

      echo json_encode($email);
      exit;
  }

  echo json_encode([]);
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use axum::{
      extract::State,
      response::{IntoResponse, Json, Response},
  };
  use resend_rs::{types::GetInboundEmailOptions, Resend};
  use serde::Serialize;
  use std::sync::Arc;

  struct AppState {
      resend: Resend,
  }

  #[derive(Serialize)]
  struct Empty {}

  async fn example(
      State(state): State<Arc<AppState>>,
      Json(event): Json<resend_rs::events::EmailEvent>,
  ) -> Response {
      if matches!(
          event.r#type,
          resend_rs::events::EmailEventType::EmailReceived
      ) {
          let email = state
              .resend
              .receiving
              .get(&event.data.email_id, GetInboundEmailOptions::default())
              .await
              .unwrap();

          dbg!(&email.html, &email.text, &email.headers);

          Json(email).into_response()
      } else {
          Json(Empty {}).into_response()
      }
  }
  ```
</CodeGroup>
