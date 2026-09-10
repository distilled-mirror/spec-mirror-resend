> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Axum

> Send your first email using Axum and the Resend Rust SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    Get the Resend Rust SDK and the [Tokio](https://tokio.rs) runtime.

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    cargo add resend-rs
    cargo add tokio -F macros,rt-multi-thread
    ```
  </Step>

  <Step title="Send an Email">
    ```rust theme={"theme":{"light":"github-light","dark":"vesper"}}
    use std::sync::Arc;

    use axum::{extract::State, http::StatusCode, routing::get, Router};
    use resend_rs::types::CreateEmailBaseOptions;
    use resend_rs::{Resend, Result};

    // Cloning the Resend client is fine and cheap as the internal HTTP client is
    // not cloned.
    #[derive(Clone)]
    struct AppState {
      resend: Resend,
    }

    #[tokio::main]
    async fn main() {
      let shared_state = Arc::new(AppState {
        resend: Resend::new("re_xxxxxxxxx"),
      });

      // build our application with a single route
      let app = Router::new()
        .route("/", get(endpoint))
        // provide the state so the router can access it
        .with_state(shared_state);

      // run our app with hyper, listening globally on port 3000
      let listener = tokio::net::TcpListener::bind("0.0.0.0:3000").await.unwrap();
      axum::serve(listener, app).await.unwrap();
    }

    async fn endpoint(State(state): State<Arc<AppState>>) -> Result<String, StatusCode> {
      let from = "Acme <onboarding@resend.dev>";
      let to = ["delivered@resend.dev"];
      let subject = "Hello World";

      let email = CreateEmailBaseOptions::new(from, to, subject)
        .with_html("<strong>It works!</strong>");

      // access the state via the `State` extractor and handle the error
      match state.resend.emails.send(email).await {
        Ok(email) => Ok(email.id.to_string()),
        Err(_) => Err(StatusCode::INTERNAL_SERVER_ERROR),
      }
    }
    ```

    Opening your browser at `http://localhost:3000` (or running `curl localhost:3000`) sends an
    email and returns its id!
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Axum App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/rust-resend-examples/axum_app">
    Full Axum web framework application
  </Card>

  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/basic_send.rs">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/with_attachments.rs">
    Send emails with file attachments
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/with_template.rs">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/scheduled_send.rs">
    Schedule emails for future delivery
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/audiences.rs">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/domains.rs">
    Create and manage sending domains
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/inbound.rs">
    Receive and process inbound emails
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/rust-resend-examples/examples/double_optin_subscribe.rs">
    Double opt-in subscription flow
  </Card>
</CardGroup>
