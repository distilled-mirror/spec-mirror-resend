> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to set up Apple Branded Mail

> Learn how to implement Apple Branded Mail to display your logo in Apple Mail clients.

export const YouTube = ({id}) => {
  return <iframe className="w-full aspect-video rounded-xl" src={`https://www.youtube.com/embed/${id}`} title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>;
};

## Prerequisites

To get the most out of this guide, you will need to:

* [Create an Apple Business Connect account](https://www.apple.com/business/connect/)
* [Setup DMARC on your domain](/docs/dashboard/domains/dmarc)
* A company identification number for Apple to verify your company

Prefer watching a video? Check out our video walkthrough below.

<YouTube id="zLDRvWVPqxk" />

## Why use Apple Branded Mail

Apple Branded Mail is a proprietary Apple format that displays your logo as an avatar in the inbox of Apple Mail. Displaying your logo can increase brand recognition and trust and improve engagement.

There are a few benefits of Apple Branded mail over BIMI:

* Since it's an Apple format, it does not require a certificate like [BIMI does](/docs/dashboard/domains/bimi).
* The image support is broader, supporting `.png`, `.heif`, and `.jpg` logos.

Since Apple Branded Mail works only with Apple Mail on new iOS, iPadOS, and macOS versions, your logo will not show in other mail clients or older versions of Apple Mail.

For this reason, follow all possible methods for adding your logo to your emails, including Apple Branded Mail, [our general guide](/docs/knowledge-base/how-do-i-send-with-an-avatar), and [BIMI](/docs/dashboard/domains/bimi) if it fits your needs.

## Implementing Apple Branded Mail

<Steps>
  <Step title="Configure DMARC">
    <Note>
      If you haven't set up DMARC yet, follow our [DMARC Setup
      Guide](/docs/dashboard/domains/dmarc).
    </Note>

    To ensure your logo appears with Apple Branded Mail, set your DMARC policy to either `p=quarantine;` or `p=reject;`. This policy guarantees that your emails are authenticated and prevents others from spoofing your domain and sending emails with your logo.

    Here's an overview of the required parameters:

    | Parameter | Purpose    | Required Value                 |
    | --------- | ---------- | ------------------------------ |
    | `p`       | Policy     | `p=quarantine;` or `p=reject;` |
    | `pct`     | Percentage | `pct=100;`                     |

    Here is an example of an adequate DMARC record:

    ```
    "v=DMARC1; p=quarantine; pct=100; rua=mailto:dmarcreports@example.com"
    ```

    As we mention in our [DMARC Setup Guide](/docs/dashboard/domains/dmarc), be sure to test your emails to make sure they are passing DMARC before changing your DMARC policy to `p=quarantine;` or `p=reject;`.
  </Step>

  <Step title="Create an Apple Business Connect account">
    Apple displays the logo you set in your Business Connect account. [Create an account](https://www.apple.com/business/connect/) if your company does not already have one. Make sure to use your company details when signing up.
  </Step>

  <Step title="Add your company details">
    Apple will prompt you to provide details like your company address and name.
  </Step>

  <Step title="Add your brand details">
    Once your company account is created, in Apple Business Connect, select the **Branded Mail** option in the left sidebar and provide details on your brand. Add details like the brand name and your brand website.

    <img src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/abm-step-4-add-brand-details-1.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=8348f2b44a70bfb6c4e065046a7443dd" alt="Add your brand details" width="3412" height="1884" data-path="images/abm-step-4-add-brand-details-1.png" />

    <img src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/abm-step-4-add-brand-details-2.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=8ae25d711442f1f38620bd0aa1996fee" alt="Add your brand details" width="3412" height="1884" data-path="images/abm-step-4-add-brand-details-2.png" />
  </Step>

  <Step title="Add your logo">
    Once you fill out the brand details, upload your logo. Apple requires the logo to be at least 1024 x 1024 px in a `.png`, `.heif`, or `.jpeg` format.

    <img src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/abm-step-5-add-your-logo.png?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=325d6466f5c237cd8c478eba3ac746d5" alt="Add your logo" width="3412" height="1884" data-path="images/abm-step-5-add-your-logo.png" />
  </Step>

  <Step title="Add your domain">
    Confirm the domains or email addresses where you want your brand logo to appear.

    You can register your logo for your root domain or a subdomain. If you don't set a specific logo for a subdomain, the root domain logo will automatically display for any email sent from your subdomains.
  </Step>

  <Step title="Verify your company">
    Apple requires details to confirm your company identity.

    If you're in the United States, provide a Federal Taxpayer Identification Number. Other countries will use a local equivalent for this step. Apple also asks that you add a DNS record to verify DNS access.
  </Step>

  <Step title="Verify with Apple">
    After you submit all your information, Apple will verify your details. This process may take up to seven business days.

    Once the logo is verified, Apple will send an email notification and note the verified status in Branded Mail. Your logo will start to display in compatible Apple Mail versions.

    <img src="https://mintcdn.com/resend/PWWYUiKcsGOVT_Rs/images/abm-step-8-verify-with-apple.png?fit=max&auto=format&n=PWWYUiKcsGOVT_Rs&q=85&s=bbf80629357b9a4df827d9911677b97d" alt="Verified logo" width="3412" height="1884" data-path="images/abm-step-8-verify-with-apple.png" />

    <Tip>
      See Apple's documentation on [Apple Branded
      Mail](https://support.apple.com/en-au/guide/apple-business-connect/abcb761b19d2/web)
      for any detailed questions on adding your logo.
    </Tip>
  </Step>
</Steps>
