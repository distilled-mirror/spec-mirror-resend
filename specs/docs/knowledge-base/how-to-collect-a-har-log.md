> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to collect a HAR log

> Capture a HAR file in Chrome or Firefox so Resend support can see what your browser sent when something failed.

A HAR (HTTP Archive) file records the requests your browser made while you used a page, including timing, headers, and responses. If something fails in the Resend dashboard, a HAR log shows support the exact requests behind that failure.

Collect the log while you reproduce the issue, with Developer Tools open.

> [!WARNING]
>
> A HAR file can include cookies, session tokens, and request bodies such as API
> keys. Share it only with [Resend support](https://resend.com/help). Don't post
> it in a public channel.

## Google Chrome

1. Open the Resend page where the problem happens.
2. Open Developer Tools. Click the three-dot menu, then **More tools** > **Developer tools**. You can also press `Ctrl`+`Shift`+`I` on Windows and Linux, or `Cmd`+`Option`+`I` on macOS.
3. Click the **Settings** gear in Developer Tools.
4. On the **Preferences** tab, under **Network**, turn on:
   * **Keep log**
   * **Disable cache (while DevTools is open)**
   * **Allow to generate HAR**
5. Under **Console**, turn on:
   * **Show timestamps**
   * **Keep log on navigation**
6. Close Settings and select the **Network** tab. Leave Developer Tools open.
7. Reproduce the issue. If the Network list is empty, reload the page and try again.
8. In the Network tab, click and hold the download icon (**Export HAR**). Save the file:
   * **Export HAR (sanitized)**

Send the file with your support request.

## Firefox

1. Open the Resend page where the problem happens.
2. Click the three-line menu in the top right, then **More tools** > **Web Developer Tools**. You can also press `Ctrl`+`Shift`+`I` on Windows and Linux, or `Cmd`+`Option`+`I` on macOS.
3. Select the **Network** tab.
4. Click the gear in the Network panel and turn on **Persist Logs**.
5. Reproduce the issue with Web Developer Tools open. If the list is empty, reload the page and try again.
6. Right-click the first row in the list and choose **Save All As HAR**.

Attach that file when you [contact support](https://resend.com/help).
