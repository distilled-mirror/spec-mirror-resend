> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How do Dedicated IPs work?

> When are Dedicated IPs helpful, and how can they be requested.

## What is a Dedicated IP?

In email delivery, the sending IP address serves as a key identifier. Inbox Providers like Gmail track the reputation of these IPs based on the quality and quantity of emails sent from them, factoring this information into filtering and inbox placement decisions.

By default, all Resend users use our shared IPs, which are a collection of IPs shared across many senders. Optionally, you can purchase a dedicated IP pool so a range of IPs are exclusively assigned to your sending.

Resend goes one step further and exclusively provisions "Managed Dedicated IP Pools". These managed pools handle multiple delicate and time consuming aspects of dedicated IPs:

* **Automatic warmup**: New IPs have no reputation and are therefore under scrutiny by inbox providers. Resend carefully migrates your sending over from the shared pool to your dedicated pool.
* **Automatic scaling**: IPs can only send at a certain rate based on the specifications of each inbox provider. Resend scales your pool dynamically based on the inbox provider feedback, without you lifting a finger.
* **Continuous monitoring**: Resend continuously monitors the reputation and performance of your dedicated IPs.
* **Fully dedicated**: You can segregate your emails from sending on shared pools to reduce risk of "noisy neighbors".

<Note>
  Resend only provisions Managed Dedicated IP Pools, but we will refer to them
  as **Dedicated IPs** in this article to be succinct.
</Note>

## When Dedicated IPs are helpful

Historically, Dedicated IPs were seen as the primary ingredient to great deliverability. This is not true anymore as Inbox Providers have incorporated dozens of other factors like sending history, domain reputation, and sending feedback (bounces and complaints) more predominantly than IP reputation.

Though Dedicated IPs are not a deliverability silver bullet, they maintain a helpful benefit: **removing risk of noisy neighbors**.

There is power in numbers, and for many senders it can be helpful to leverage the positive reputation of other senders in an IP pool. For some senders though, they want to maintain their own IP reputation without any chance of being impacted, positively or negatively, by other senders. For them, Dedicated IPs are a helpful solution.

## When Dedicated IPs are not helpful

Dedicated IPs can be helpful, but there are some situations where they can actually hinder your ability to reach the inbox. If any of these situations match your use case, Dedicated IPs may hinder more than help:

* **Low email volume**: Sending less than 90,000 emails a month may not be enough to keep the IPs warm.
* **Inconsistent sending**: Sudden changes in email volume can hurt your IP reputation.
* **Poor email practices**: A Dedicated IP exposes your sending behavior even more.
* **New sender**: If you're starting out and have no sending history.
* **IP Allowlisting**: Resend does not expose the IPs included in your dedicated pool.

## How IP warmup works

With Resend's Managed Dedicated IP Pools, the warmup process is handled automatically:

1. **Automatic scaling**: Add or remove IP addresses based on your sending volume.
2. **Gradual increase**: Gradually increase the volume of emails sent through new IPs over time.
3. **Traffic distribution**: During warmup, traffic is distributed across shared and dedicated IPs.
4. **Reputation monitoring**: Continuously monitor the reputation of your dedicated IPs.
5. **Adaptive warmup**: Adapt the warmup process to your sending patterns.

Often IP warmup is a highly manual process and requires great care if you don't want a deliverability degradation in the process. With this automatic warmup process, that's handled for you so you can focus on sending.

<Note>
  Because Managed Dedicated IP Pools are dynamically scaled, **we do not expose
  the list of IPs** in your dedicated pool.
</Note>

## Requirements for a Dedicated IP

You can request a Dedicated IP if you meet the following requirements:

* Your domains are in the same region (Dedicated IPs are provisioned per region).
* Your sending volume exceeds 3,000 emails sent per day.
* You already have an active Transactional Scale or Marketing Pro subscription.
* All domains you want added to the Dedicated IP are already verified on Resend.

## How to request a Dedicated IP

If you're on a Scale plan or higher, you can request a Dedicated IP directly from your dashboard:

1. Navigate to **Settings** > **Usage**
2. Click **Request dedicated IP** in the Dedicated IPs section
3. Fill out the request form with information about your sending patterns

Alternatively, you can request a Dedicated IP by [chatting with support](https://resend.com/help).

You will need to provide the following information:

* What types of emails are you sending?
* How many emails are you sending per day and month on average?
* Is your sending consistent every day, or do you send in bursts?
* Which domains do you want included in your Dedicated IP?
