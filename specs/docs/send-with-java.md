> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Java

> Learn how to send your first email using the Resend Java SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key.md)
* A [verified domain](/docs/add-a-domain.md)

## Guide

**1. Install**

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

**2. Send emails using HTML**

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

## Examples

> **[Basic Send](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/BasicSend.java)**
>
> Basic email sending

> **[Attachments](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/WithAttachments.java)**
>
> Send emails with file attachments

> **[Templates](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/WithTemplate.java)**
>
> Send emails using Resend hosted templates

> **[Scheduling](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/ScheduledSend.java)**
>
> Schedule emails for future delivery

> **[Audiences](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/Audiences.java)**
>
> Manage contacts and audiences

> **[Domains](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/Domains.java)**
>
> Create and manage sending domains

> **[Inbound Webhooks](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/Inbound.java)**
>
> Receive and process inbound emails

> **[Double Opt-in](https://github.com/resend/resend-examples/blob/main/java-resend-examples/src/main/java/com/resend/examples/DoubleOptinSubscribe.java)**
>
> Double opt-in subscription flow

> **[Javalin App](https://github.com/resend/resend-examples/tree/main/java-resend-examples/javalin_app)**
>
> Full Javalin web framework application

> **[Spring Boot App](https://github.com/resend/resend-examples/tree/main/java-resend-examples/spring_boot_app)**
>
> Full Spring Boot application
