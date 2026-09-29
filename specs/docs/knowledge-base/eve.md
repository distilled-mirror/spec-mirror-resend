> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Eve

> Connect to your Eve agent over email.

[Eve](https://eve.dev/) is an open-source framework for building agents created by Vercel. It's filesystem-first, inspired by Next.js, and provides tools, workflows, connections, hooks, and channels for you to build long-running, durable agents.

Using the [Resend adapter for the Vercel Chat SDK](/docs/chat-sdk) you can plug in email as a channel to your eve agent.

## Prerequisites

To get started, you'll need to:

* [Create an API key](https://resend.com/api-keys)
* [Verify your domain](https://resend.com/domains)
* [Set up webhooks](/docs/webhooks/introduction) for `email.received` events
* [Enable receiving](/docs/dashboard/receiving/introduction) on your domain

## Guide

<Steps>
  <Step title="Install">
    Create a new project with eve and then install the Chat SDK, the Resend adapter, and the development state adapter.

    <CodeGroup>
      ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
      npx eve@latest init my-agent
      cd my-agent
      npm install @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```

      ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
      yarn dlx eve@latest init my-agent
      cd my-agent
      yarn add @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```

      ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
      pnpm dlx eve@latest init my-agent
      cd my-agent
      pnpm add @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```

      ```bash bun theme={"theme":{"light":"github-light","dark":"vesper"}}
      bunx eve@latest init my-agent
      cd my-agent
      bun add @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```
    </CodeGroup>
  </Step>

  <Step title="Configure the adapter">
    Create the Resend adapter with the [adapter configuration options](#configuration-options). Then create a Chat SDK channel with the adapter, a username for the bot, and an adapter state. `streaming` should be set to false as emails can only deliver one message per turn.

    Export the `channel` object and the framework will integrate it automatically.

    ```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    import { createResendAdapter } from '@resend/chat-sdk-adapter';
    import { chatSdkChannel } from 'eve/channels/chat-sdk';
    import { createMemoryState } from '@chat-adapter/state-memory';

    export const resendAdapter = createResendAdapter({
      fromAddress: 'bot@example.com',
      fromName: 'My Bot',
    });

    export const { bot, channel, send } = chatSdkChannel({
      adapters: { resend: resendAdapter },
      userName: 'My Bot',
      state: createMemoryState(),
      streaming: false,
    });

    export default channel;
    ```

    <Info>
      Set `RESEND_API_KEY` and `RESEND_WEBHOOK_SECRET` as environment variables. You can also pass `apiKey` and `webhookSecret` directly in the config passed to `createResendAdapter` — explicit values take precedence over env vars.
    </Info>
  </Step>

  <Step title="Handle new messages">
    Register handlers for incoming messages. `onNewMention` event fires when a new thread starts and `onSubscribedMessage` fires for follow-up emails in threads you are already subscribed to.

    ```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    bot.onNewMention(async (thread, message) => {
      await thread.subscribe();
      await send(message.text, { thread });
    });
    bot.onSubscribedMessage(async (thread, message) => {
      await send(message.text, { thread });
    });
    ```

    Threading is handled by the [Chat SDK adapter](/docs/chat-sdk#how-threading-works).
  </Step>

  <Step title="Configure webhooks">
    Eve registers adapter endpoints at `/eve/v1/resend`. [Edit your webhook](/docs/webhooks/introduction) for `email.received` events to point to this endpoint.
  </Step>
</Steps>

## Configuration options

| Parameter | Type | Required | Description |
| - | - | - | - |
| `fromAddress` | `string` | Yes | Sender email address |
| `fromName` | `string` | No | Display name for the From header |
| `apiKey` | `string` | No | Resend API key. Falls back to `RESEND_API_KEY` env var |
| `webhookSecret` | `string` | No | Webhook signing secret. Falls back to `RESEND_WEBHOOK_SECRET` env var |
