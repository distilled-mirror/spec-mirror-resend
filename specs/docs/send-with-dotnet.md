> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with .NET

> Learn how to send your first email using the Resend .NET SDK.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

Prefer watching a video? Check out our video walkthrough below.

[YouTube video player](https://www.youtube.com/embed/HvFURxq1tgQ)

## Guide

**1. Install**

```bash dotnet CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
dotnet add package Resend
```

```bash Visual Studio (Package Manager Console) theme={"theme":{"light":"github-light","dark":"vesper"}}
PM> Install-Package Resend
```

**2. Send emails using HTML**

In the startup of your application, configure the DI container as follows:

```csharp theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

builder.Services.AddOptions();
builder.Services.AddHttpClient<ResendClient>();
builder.Services.Configure<ResendClientOptions>( o =>
{
    o.ApiToken = Environment.GetEnvironmentVariable( "RESEND_APITOKEN" )!;
} );
builder.Services.AddTransient<IResend, ResendClient>();
```

Send an email using the injected `IResend` instance:

```csharp theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

public class FeatureImplementation
{
    private readonly IResend _resend;


    public FeatureImplementation( IResend resend )
    {
        _resend = resend;
    }


    public Task Execute()
    {
        var message = new EmailMessage();
        message.From = "Acme <onboarding@resend.dev>";
        message.To.Add( "delivered@resend.dev" );
        message.Subject = "hello world";
        message.HtmlBody = "<strong>it works!</strong>";

        await _resend.EmailSendAsync( message );
    }
}
```

## Examples

> **[Basic Send](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/BasicSend.cs)**
>
> Basic email sending

> **[Attachments](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/WithAttachments.cs)**
>
> Send emails with file attachments

> **[Templates](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/WithTemplate.cs)**
>
> Send emails using Resend hosted templates

> **[Scheduling](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/ScheduledSend.cs)**
>
> Schedule emails for future delivery

> **[Audiences](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/Audiences.cs)**
>
> Manage contacts and audiences

> **[Domains](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/Domains.cs)**
>
> Create and manage sending domains

> **[Inbound Webhooks](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/Inbound.cs)**
>
> Receive and process inbound emails

> **[Double Opt-in](https://github.com/resend/resend-examples/blob/main/dotnet-resend-examples/Examples/DoubleOptinSubscribe.cs)**
>
> Double opt-in subscription flow

> **[Minimal API App](https://github.com/resend/resend-examples/tree/main/dotnet-resend-examples/MinimalApiApp)**
>
> ASP.NET Minimal API application

> **[MVC App](https://github.com/resend/resend-examples/tree/main/dotnet-resend-examples/MvcApp)**
>
> ASP.NET MVC application
