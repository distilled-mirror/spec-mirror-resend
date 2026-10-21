> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create an API key

> Get started sending emails by creating an API key

## Resend API keys

API Keys are secret tokens used to authenticate your requests. They are unique to your account and must be kept confidential.

You must create at least one API key to use the Resend platform through code (e.g., SDKs, API, command-line interface (CLI), or AI tools).

## Create an API Key

You can create API keys in four ways:

* in the [**API keys** Dashboard page](/docs/dashboard/api-keys/introduction)
* using the [Resend API](/docs/api-reference/api-keys/create-api-key)
* with a [Resend CLI command](/docs/cli#api-keys)
* with the [Resend MCP server](/docs/mcp-server)

To create a new API Key from the Resend Dashboard:

**1. In your Resend Dashboard, navigate to the API keys page.**

**2. Click the Create API Key button.**

**3. Provide a name for your API Key.**

Choose a name (maximum 50 characters) to identify your key.

**4. Select a permission for your API key.**

Choose **"Sending access"** to grant access to only sending emails unless your key needs full access to Resend’s API to create, delete, get, and update any resource.

This [API key permission](/docs/api-reference/api-keys/create-api-key#param-permission) can be updated at any time [in the Dashboard](/docs/dashboard/api-keys/introduction#edit-api-key-details).

**5. (Optional) Restrict sending to a specific domain**

If you selected **"Sending access"**, you can further choose the domain you want to restrict access to.

![Add API Key modal in the Resend Dashboard](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-add.png?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=1ecfaf7a2d2a780b826f941078e427b5)

> [!NOTE]
>
> For security reasons, you can only view the API Key once. Learn more about
> [API key best practices](/docs/knowledge-base/how-to-handle-api-keys).

## Use the API key in your code

Authenticate your requests by adding your Resend API key to your project as an environment variable.

You can check the [quickstart guides](/docs/introduction) or [AI builder guides](/docs/ai-onboarding#ai-builder-guides) for specific examples of passing your API key to your project.

**1. Create and store an environment variable**

Store your API key as an environment variable in your project. This is commonly done inside a special file or configuration panel and will depend on your language, framework, or development platform.

For example, Node.js projects commonly store both public and secret variables in a `.env` file at the root of your project:

```sh .env theme={"theme":{"light":"github-light","dark":"vesper"}}
RESEND_API_KEY=re_xxxxxxxxx
```

> [!TIP]
>
> If you are storing your secrets in a project file, you may need to add this file to your `.gitignore` file to prevent it from being committed to version control.
>
> Many frameworks add `.env` to the `.gitignore` file by default, so this may already exist.
>
> ```ts .gitignore theme={"theme":{"light":"github-light","dark":"vesper"}}
> .env
> ```

**2. Pass the environment variable to your code**

Your project environment variables are not automatically available to Resend. You must explicitly pass your API key value to your Resend code.

For example, whenever you create a new Resend instance in a Node.js project, you must pass the environment variable on `process.env`:

```ts app.ts theme={"theme":{"light":"github-light","dark":"vesper"}}
const resend = new Resend(process.env.RESEND_API_KEY);
```

> [!NOTE]
>
> On Node.js `v20` and later, you can pass your `.env` file's variables to your script using the `--env-file=.env` flag. Alternatively, you can use the `dotenv` package to load the variables.

## Learn more

> **[Manage API keys](/docs/dashboard/api-keys/introduction)**
>
> View, create, edit, delete, and manage your API keys.

> **[API key best practices](/docs/knowledge-base/how-to-handle-api-keys)**
>
> Learn about best practices for managing your API keys.

## Next steps

> **[Add a domain](/docs/add-a-domain)**
>
> Add and verify a domain you own to start sending emails.

> **[Quickstart tutorials](/docs/introduction)**
>
> Send your first transactional email with a quick tutorial for your language
> or framework.
