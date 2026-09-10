> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to fix CORS issues

> Information on recommended options to avoid CORS errors when sending emails.

## Problem

It's common for people to hit CORS (Cross-Origin Resource Sharing) issues when using the Resend API. This error typically shows as:

```
Access to XMLHttpRequest at 'https://api.resend.com/emails'
from origin 'http://localhost:3000' has been blocked by CORS policy:
Response to preflight request doesn't pass access control check:
No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

## Solution

Usually CORS errors happens when you're sending emails from the **client-side**.

Send the emails on the **server-side** to not expose your API keys and avoid CORS issues.
