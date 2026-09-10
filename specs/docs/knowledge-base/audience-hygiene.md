> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Audience Hygiene: How to keep your Audiences in good shape?

> Learn strategies for maintaining good audience hygiene and maximizing email deliverability.

Audience hygiene (*also known as list hygiene*) refers to the practice of keeping your email list clean, valid, and engaged.

Maintaining proper audience hygiene is crucial for ensuring that your emails reach their intended recipients, maximizing your deliverability, and improving your sender reputation.

By removing invalid, outdated, or disengaged contacts, you can improve the effectiveness of your email campaigns. You'll also avoid issues like high bounce rates, low engagement, and even being marked as spam.

***

# How to ensure emails are valid

To keep your list healthy, it's essential to ensure that the email addresses you collect are valid, accurate, and belong to recipients who are truly interested in hearing from you. Here are a few strategies to help you achieve this:

### Prevent undesired or bot signups with CAPTCHA

Bots can sign up for your emails with little friction, inflating your list with fake or low-quality contacts. To help protect against bot signups, implement CAPTCHA systems during the sign-up process. CAPTCHA challenges help ensure that sign-ups come from human users and not bots or automated scripts.

Some popular CAPTCHA services include:

* **[Google reCAPTCHA](https://developers.google.com/recaptcha)**: One of the most widely used CAPTCHA services, offering both simple and advanced protection options.
* **[hCaptcha](https://www.hcaptcha.com/)**: An alternative to Google reCAPTCHA, providing similar protection but with a different user experience.
* **[Friendly Captcha](https://friendlycaptcha.com/)**: A privacy-focused CAPTCHA solution that doesn’t require users to click on anything, reducing friction in the sign-up process.

Using these tools will help reduce bot sign-ups and ensure your email list consists of real users.

### Ensure the recipient is consenting with Double Opt-In

Double opt-in is the process of confirming a user's subscription after they’ve signed up for your emails.

When a user submits their email address, you send them a confirmation email with a link they must click to complete the subscription process.

This step ensures that the person who entered the email address is the one who actually wants to receive your communications.

This is important to ensure:

* **Compliance with local regulations**: Double opt-in helps ensure that you comply with email marketing regulations such as the **CAN-SPAM Act** (U.S.) and **CASL** (Canada). Both of these laws require clear consent from subscribers before you can send them marketing emails.
* **Improved deliverability**: Double opt-in helps you maintain a clean list of genuinely interested users. This reduces bounce rates and prevents spam complaints, which in turn helps maintain your sender reputation with ISPs and inbox providers.
* **Verification of accuracy**: Double opt-in ensures the email addresses you collect are valid, accurate, and up to date, reducing the risk of sending to invalid addresses and impacting your deliverability.

### Use a third-party service to verify an address' deliverability

While you can verify that an email address follows the correct syntax (e.g., [user@example.com](mailto:user@example.com)) (also known as RFC 5322), you also need to ensure that the address is deliverable, that is, it’s an active inbox that can receive emails.

Third-party email verification services can help you identify whether an email address is valid, reachable, or likely to result in a bounce.

This reduces the risk of sending to addresses that won’t receive your emails and improves your overall deliverability.

Some email verification services include:

* **[Emailable](https://emailable.com/partners/resend)**
* **ZeroBounce**
* **Kickbox**

By using these services, you can clean up your existing email lists or prevent undeliverable emails to be added to them. This helps prevent unnecessary deliverability issues.

***

# How to proactively remove emails from your Segments

Over time, certain recipients may become disengaged with your content. It's important to manage your segments by removing inactive or unengaged users.

Regularly filtering your segments ensures that you're sending to only those who are actively interested, which in turn boosts engagement and deliverability.

A healthy email list is one that is continuously nurtured with relevant and timely content. Instead of sporadic communication, maintain consistent engagement with your audience to keep them interested.

### Filter on engagement

To keep your email list in top shape, focus on sending to engaged users. Major inbox providers like Gmail and Microsoft expect you to send emails to recipients who have recently opened or clicked on your emails.

As a best practice, limit non-transactional email sends to recipients who have opened or clicked an email in the past 6 months.

<Info>
  The exact timeframe may vary depending on your industry, sending frequency,
  and audience behavior, but 6 months is a generally accepted standard.
</Info>

Regularly cleaning your list of disengaged recipients helps maintain a positive sender reputation and boosts your chances of landing in the inbox instead of the spam folder.

### Automatically remove bounced recipients

Using our [Webhooks](/docs/webhooks/introduction), you can be notified when a delivery bounces or gets marked as spam by the recipient.

This allows you to proactively unsubscribe the recipient and prevent further sending. Resend will automatically suppress further deliveries to that email address but will not automatically unsubscribe it for you.

### Sunset unengaged recipients

If certain recipients have not engaged with your emails over an extended period (e.g., 6+ months), consider removing them from your Marketing sends.

Continuing to send to these unengaged users can harm your deliverability by increasing bounce rates and decreasing your open rates.

To re-engage these users, you may want to send a re-engagement campaign or offer an incentive for them to stay on your list. If they don't respond, it's often best to remove them to keep your list healthy and avoid wasting resources on inactive contacts.

***

Audience hygiene involves validating email addresses, ensuring consent, verifying deliverability, and removing unengaged recipients. By maintaining these practices, you'll improve your email deliverability and foster better relationships with your subscribers.

This will help you achieve better engagement rates and a healthier sender reputation with inbox providers.
