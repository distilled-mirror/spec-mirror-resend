> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Domain and/or IP Warm-up Guide

> Learn how to warm up a domain or IP to avoid deliverability issues.

Warming up a domain or IP refers to the practice of progressively increasing your sending volume to maximize your deliverability. The goal is to send at a consistent rate and avoid any spikes in email volume that might be concerning to inbox service providers.

Whenever you change your sending patterns, warm up your domain and/or IP. This applies when you use a new domain, a new IP, or a new vendor, or when your volume will increase.

A thought-out warm-up plan limits greylisting and delivery throttling, as well as helping establish a good domain and IP reputation.

As your volume increases, you'll need to monitor your bounce rate to ensure it remains below 4%, and your spam rate below 0.08%. An increase in these rates would be a sign that your warm-up plan needs to be slowed down and an investigation into the root causes of the increases started.

Following these rules and metrics will establish a good domain reputation.

> [!NOTE]
>
> Each sender has different constraints and needs, so these numbers are meant as
> a baseline. Our [Support team](https://resend.com/help) can work with you on
> devising a plan adapted to your needs.

## Existing domain

If you're already sending from an existing domain with established reputation and volumes, you can use the following guidelines to start sending with Resend.

| **Day** | **Messages per day** | **Messages per hour** |
| - | - | - |
| **1** | Up to 1,000 emails | 100 Maximum |
| **2** | Up to 2,500 emails | 300 Maximum |
| **3** | Up to 5,000 emails | 600 Maximum |
| **4** | Up to 5,000 emails | 800 Maximum |
| **5** | Up to 7,500 emails | 1,000 Maximum |
| **6** | Up to 7,500 emails | 1,500 Maximum |
| **7** | Up to 10,000 emails | 2,000 Maximum |

## New domain

Before you start sending emails with a brand new domain, it's especially important to have a warm-up plan so you can maximize your deliverability right from the start.

| **Day** | **Messages per day** | **Messages per hour** |
| - | - | - |
| **1** | Up to 150 emails | |
| **2** | Up to 250 emails | |
| **3** | Up to 400 emails | |
| **4** | Up to 700 emails | 50 Maximum |
| **5** | Up to 1,000 emails | 75 Maximum |
| **6** | Up to 1,500 emails | 100 Maximum |
| **7** | Up to 2,000 emails | 150 Maximum |

## Warm-up calculator

Use the calculator below to generate a personalized warm-up schedule based on your specific needs. Enter your target volume, timeline, and domain type to get a custom plan.

The guide is meant as a general plan, but always pay careful attention to your deliverability and adjust accordingly. If you have specific questions, [please reach out to us](https://resend.com/help).

Domain Type

<input type="radio" name="domainType" value="new" checked={domainType === 'new'} onChange={(e => setDomainType(e.target.value))} />

New Domain

<input type="radio" name="domainType" value="existing" checked={domainType === 'existing'} onChange={(e => setDomainType(e.target.value))} />

Existing Domain

Target Daily Volume

<input id="targetVolume" type="number" min="100" max="1000000" step="100" value={targetVolume} onChange={(e => setTargetVolume(Number(e.target.value)))} placeholder="e.g., 5000" />

Start Date

<input id="startDate" type="date" value={startDate} onChange={(e => setStartDate(e.target.value))} />

Target Date (optional)

<input id="targetDate" type="date" value={targetDate} onChange={(e => setTargetDate(e.target.value))} min={startDate} />

Warm-up Duration

days

Start Date

Full Capacity Date

Target Volume

/day

**Day**

**Date**

**Messages per day**

**Messages per hour**

Tip

As you warm up, keep your **bounce rate below 4%** and
your **spam rate below 0.08%**. If these rates increase,
slow down your warm-up and investigate the root cause before
continuing.

# Warming up your Dedicated IP with Resend

In order for a Dedicated IP to be beneficial or useful, you first need to establish a certain sending volume and patterns. Once you've established this volume and these patterns, our [Support team](https://resend.com/help) can set it up for you.

Resend provides an automatic warm-up process so that you can focus on sending.

[Learn more about requesting a Dedicated IP](https://resend.com/docs/knowledge-base/how-do-dedicated-ips-work#how-to-request-a-dedicated-ip).

# Third-party warm-up services

Email deliverability is important, and it can be tempting to use services promising quick fixes. However, using tools that artificially boost engagement can harm your long-term sender reputation. These services often rely on manipulating anti-spam filters, which can backfire as email providers like Gmail adjust their systems.

Instead, focus on sustainable practices, such as sending relevant content, maintaining a clean list, and using proper authentication. These methods build trust with email providers and improve your deliverability over time.
