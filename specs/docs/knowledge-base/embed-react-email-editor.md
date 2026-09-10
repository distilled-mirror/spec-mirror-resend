> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Embed the React Email editor in your app

> Add the open-source React Email editor to your application: base component, styling, Inspector sidebar, and custom extensions.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

The [React Email editor](https://react.email/docs/editor/overview) is an open-source visual editor that lets your users author email templates inside your own product. It ships with bubble menus, slash commands, an Inspector sidebar, and extensible nodes. It also exports email-ready HTML you can hand straight to Resend.

This guide walks through embedding the editor in a React app, styling it to match your brand, customizing the Inspector Sidebar, and adding your own custom node.

<YouTube id="zhIT3NYEcMw" />

## Prerequisites

* A React 18+ application (for example, Vite, Next.js, or Remix)
* A bundler with [package exports](https://nodejs.org/api/packages.html#exports) support (the defaults for the frameworks above)

<Steps>
  <Step title="Install the editor">
    Install `@react-email/editor` and import the bundled theme stylesheet once at your app root.

    <CodeGroup>
      ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
      npm install @react-email/editor
      ```

      ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
      yarn add @react-email/editor
      ```

      ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
      pnpm add @react-email/editor
      ```

      ```bash bun theme={"theme":{"light":"github-light","dark":"vesper"}}
      bun add @react-email/editor
      ```
    </CodeGroup>

    ```tsx app/layout.tsx theme={"theme":{"light":"github-light","dark":"vesper"}}
    import '@react-email/editor/themes/default.css';
    ```

    The bundled theme covers the bubble menus, slash commands, and Inspector. If you only use a subset, you can [import individual stylesheets](https://react.email/docs/editor/getting-started#import-css) instead.
  </Step>

  <Step title="Mount the base editor">
    The fastest path is the standalone `EmailEditor` component. It comes with the default extensions, bubble menus, slash commands, and theming wired up.

    ```tsx app/components/Editor.tsx theme={"theme":{"light":"github-light","dark":"vesper"}}
    'use client';

    import { EmailEditor } from '@react-email/editor';

    const initialContent = `
      <h1>Welcome</h1>
      <p>Type "/" for a command, or select text to format it.</p>
    `;

    export function Editor() {
      return <EmailEditor content={initialContent} />;
    }
    ```

    `content` accepts an HTML string or a TipTap JSON document. See the [`EmailEditor` API reference](https://react.email/docs/editor/api-reference/email-editor) for the full prop list.

    <Tip>
      If you need full control over which extensions load, the provider layout, or
      the UI overlays, drop down to the [lower-level
      setup](https://react.email/docs/editor/getting-started#lower-level-setup) with
      `EditorProvider` from `@tiptap/react`.
    </Tip>
  </Step>

  <Step title="Style the editor">
    The editor exposes two layers of styling:

    1. **Editor chrome** (bubble menus, slash command palette, Inspector controls) — driven by CSS custom properties (`--re-*`) and `data-re-*` attribute selectors.
    2. **Editor content** (what the user is typing) — uses TipTap's `.tiptap` root class. Note that styling here only affects the in-editor preview; the exported HTML is styled by the [theming system](https://react.email/docs/editor/features/theming).

    Override the CSS variables on a wrapper class to apply your brand:

    ```css app/styles/editor.css theme={"theme":{"light":"github-light","dark":"vesper"}}
    .brand-editor {
      --re-bg: #fafaf9;
      --re-border: #d6d3d1;
      --re-text: #1c1917;
      --re-text-muted: #78716c;
      --re-hover: rgba(28, 25, 23, 0.04);
      --re-active: rgba(28, 25, 23, 0.08);
      --re-radius: 0.5rem;
      --re-radius-sm: 0.25rem;
    }

    /* Target a specific bubble menu button */
    [data-re-bubble-menu-item][data-active] {
      background: #2563eb;
      color: #fff;
    }

    /* Style the user's content area inside the editor */
    .tiptap h1 {
      font-size: 1.75rem;
      letter-spacing: -0.025em;
    }
    ```

    ```tsx theme={"theme":{"light":"github-light","dark":"vesper"}}
    <div className="brand-editor">
      <EmailEditor content={initialContent} />
    </div>
    ```

    The default theme also responds to `prefers-color-scheme: dark` and to a `.dark` class on any ancestor — so it works with libraries like `next-themes` out of the box. See the [Styling reference](https://react.email/docs/editor/features/styling) for the complete list of variables, `data-re-*` selectors, and content classes.
  </Step>

  <Step title="Add the Inspector Sidebar">
    The Inspector is a contextual sidebar that swaps panels based on the user's current selection — document defaults when nothing is focused, node properties when a block is selected, text formatting when text is selected.

    Pass `Inspector.Root` as a child of `EmailEditor` so it shares the editor's context:

    ```tsx app/components/Editor.tsx theme={"theme":{"light":"github-light","dark":"vesper"}}
    'use client';

    import { EmailEditor } from '@react-email/editor';
    import { Inspector } from '@react-email/editor/ui';

    export function Editor() {
      return (
        <div className="flex" style={{ height: '600px' }}>
          <EmailEditor
            content="<h1>Hello</h1><p>Click any element to inspect it.</p>"
            className="flex-1 min-w-0 overflow-y-auto p-4"
          >
            <Inspector.Root className="w-72 shrink-0 border-l p-4 overflow-y-auto">
              <Inspector.Breadcrumb />
              <Inspector.Document />
              <Inspector.Node />
              <Inspector.Text />
            </Inspector.Root>
          </EmailEditor>
        </div>
      );
    }
    ```

    See the [Inspector reference](https://react.email/docs/editor/features/inspector) for every render-prop helper, the full list of reusable section components (`Inspector.Size`, `Inspector.Padding`, `Inspector.Border`, `Inspector.Typography`, `Inspector.Background`, `Inspector.Link`), and runnable examples.
  </Step>

  <Step title="Add a custom extension">
    Custom blocks use `EmailNode`, which extends TipTap's `Node` with the `renderToReactEmail` method so the same node renders correctly inside the editor and in the exported email.

    <Info>
      See [Custom
      Extensions](https://react.email/docs/editor/advanced/custom-extensions) for
      the full API and a worked example.
    </Info>
  </Step>

  <Step title="Send the result with Resend">
    If you use the standalone `EmailEditor` component, you can access the email HTML and plain text through ref methods. In your handler, send the HTML to Resend using the [Send Email](/docs/api-reference/emails/send-email) or [Send Batch Emails](/docs/api-reference/emails/send-batch-emails) API.

    ```tsx theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}}
    import { EmailEditor, type EmailEditorRef } from '@react-email/editor';
    import { useRef, useState } from 'react';

    export function MyEditor() {
      const ref = useRef<EmailEditorRef>(null);

      const handleExport = async () => {
        if (!ref.current) return;
        const html = await ref.current.getEmailHTML();
        // Send email using Resend using a server-side API endpoint/action
        const response = await fetch('/api/send-email', {
          method: 'POST',
          body: JSON.stringify({ html }),
        });
      };

      return (
        <div>
          <EmailEditor ref={ref} content="<p>Edit me</p>" />
          <button onClick={handleExport}>Export HTML</button>
        </div>
      );
    }
    ```

    The ref exposes three export methods:

    | Method           | Returns                   | Description           |
    | ---------------- | ------------------------- | --------------------- |
    | `getEmailHTML()` | `Promise<string>`         | Email-ready HTML      |
    | `getEmailText()` | `Promise<string>`         | Plain text version    |
    | `getEmail()`     | `Promise<{ html, text }>` | Both in a single call |

    All three use [composeReactEmail](https://react.email/docs/editor/api-reference/compose-react-email) under the hood.

    <Info>
      See [Email Export docs](https://react.email/docs/editor/features/email-export)
      for more information on the export methods.
    </Info>
  </Step>
</Steps>

## Next steps

<CardGroup cols={2}>
  <Card title="React Email editor reference" icon="book" href="https://react.email/docs/editor/overview">
    The complete API surface — extensions, UI components, theming, and image
    upload.
  </Card>

  <Card title="Editor styling reference" icon="palette" href="https://react.email/docs/editor/features/styling">
    Every CSS variable and `data-re-*` selector you can target.
  </Card>

  <Card title="Custom extensions" icon="code" href="https://react.email/docs/editor/advanced/custom-extensions">
    Wrap existing TipTap extensions or build new email-safe nodes and marks.
  </Card>

  <Card title="Template emails with React Email" icon="pen-to-square" href="/docs/knowledge-base/template-emails-with-react-email">
    Author templates as `.tsx` files and upload them to Resend with the CLI.
  </Card>
</CardGroup>
