> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Java

> Learn how to send your first email using the Resend Java SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

<Steps>
  <Step title="Install">
    <CodeGroup>
      ```bash Gradle theme={"theme":{"light":"github-light","dark":"vesper"}}
      implementation 'com.resend:resend-java:+'
      ```

      ```xml Maven theme={"theme":{"light":"github-light","dark":"vesper"}}
      <dependency>
          <groupId>com.resend</groupId>
          <artifactId>resend-java</artifactId>
          <version>LATEST</version>
      </dependency>
      ```
    </CodeGroup>
  </Step>

  <Step title="Send emails using HTML">
    ```java Main.java theme={"theme":{"light":"github-light","dark":"vesper"}}
    import com.resend.*;

    public class Main {
        public static void main(String[] args) {
            Resend resend = new Resend("re_xxxxxxxxx");

            CreateEmailOptions params = CreateEmailOptions.builder()
                    .from("Acme <onboarding@resend.dev>")
                    .to("delivered@resend.dev")
                    .subject("it works!")
                    .html("<strong>hello world</strong>")
                    .build();

             try {
                CreateEmailResponse data = resend.emails().send(params);
                System.out.println(data.getId());
            } catch (ResendException e) {
                e.printStackTrace();
            }
        }
    }
    ```
  </Step>
</Steps>

## Examples

<CardGroup cols={3}>
  <Card title="Basic Send" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/BasicSend.java">
    Basic email sending
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/WithAttachments.java">
    Send emails with file attachments
  </Card>

  <Card title="Templates" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/WithTemplate.java">
    Send emails using Resend hosted templates
  </Card>

  <Card title="Scheduling" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/ScheduledSend.java">
    Schedule emails for future delivery
  </Card>

  <Card title="Audiences" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/Audiences.java">
    Manage contacts and audiences
  </Card>

  <Card title="Domains" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/Domains.java">
    Create and manage sending domains
  </Card>

  <Card title="Inbound Webhooks" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/Inbound.java">
    Receive and process inbound emails
  </Card>

  <Card title="Double Opt-in" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/DoubleOptinSubscribe.java">
    Double opt-in subscription flow
  </Card>

  <Card title="Javalin App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/java-resend-examples/javalin_app">
    Full Javalin web framework application
  </Card>

  <Card title="Spring Boot App" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/java-resend-examples/spring_boot_app">
    Full Spring Boot application
  </Card>
</CardGroup>
