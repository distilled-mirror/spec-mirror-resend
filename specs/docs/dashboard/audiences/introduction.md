> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Your Resend Audience

> Learn how to manage your Contacts and send personalized Broadcasts to them.

The [Audience Page](https://resend.com/audience) is for your marketing Broadcasts and provides tools for managing your Contacts and sending personalized Broadcasts to them. [Broadcasts](/docs/dashboard/broadcasts/introduction) also handle all your unsubscribe flows for you automatically.

The Audience page includes four areas:

* [Contacts](#contacts): individual email addresses
* [Properties](#properties): custom properties for your Contacts
* [Segments](#segments): groups of Contacts for your organization
* [Topics](#topics): user-facing tools for managing email preferences

<img src="https://mintcdn.com/resend/2SHIfycCcJlAJEpt/images/audiences-contacts-intro.png?fit=max&auto=format&n=2SHIfycCcJlAJEpt&q=85&s=82101b2b495815ad50f8b7eb823876bd" alt="Contacts" class="extraWidth" width="3736" height="1916" data-path="images/audiences-contacts-intro.png" />

## Contacts

Contacts in Resend are global entities linked to a specific email address.

<img src="https://mintcdn.com/resend/2SHIfycCcJlAJEpt/images/audiences-properties-intro.png?fit=max&auto=format&n=2SHIfycCcJlAJEpt&q=85&s=001cb276f96ad54b6a64042eada0c9c3" alt="Properties" class="extraWidth" width="3736" height="1916" data-path="images/audiences-properties-intro.png" />

Each Contact:

* is associated with a single email address
* can have custom properties
* can be in zero, one or multiple Segments
* can be opted in or out of Topics

Each Contact shows a history of all marketing interactions with the Contact.

You can import Contacts in bulk from a CSV (up to 200MB) using either the [dashboard](/docs/dashboard/audiences/contacts) or the [Contacts Import API](/docs/api-reference/contacts/create-contact-import) and SDKs. Both map CSV columns to Contact Properties (the dashboard uses AI to suggest matches and create new properties for you). API and SDK imports let you choose whether to `upsert` or `skip` existing Contacts.

Learn more about [Contacts](/docs/dashboard/audiences/contacts).

## Properties

Contact Properties can be used to store additional information about your Contacts and then personalize your Broadcasts.

<img src="https://mintcdn.com/resend/2SHIfycCcJlAJEpt/images/contact-properties.png?fit=max&auto=format&n=2SHIfycCcJlAJEpt&q=85&s=6eb917dc7ac58dd515c033cf443e0734" alt="Properties" class="extraWidth" width="3736" height="1916" data-path="images/contact-properties.png" />

Resend includes a few default properties:

* `first_name`: The first name of the contact.
* `last_name`: The last name of the contact.
* `unsubscribed`: Whether the contact is unsubscribed from all Broadcasts.
* `email`: The email address of the contact.

You can create additional custom Contact Properties for your Contacts to store additional information. These properties can be used to personalize your Broadcasts across all Segments.

Learn more about [Contact Properties](/docs/dashboard/audiences/properties).

## Segments

Segments are groups of Contacts for your organization. You can use Segments to send emails to a specific group of Contacts using [Broadcasts](/docs/dashboard/broadcasts/introduction).

<img src="https://mintcdn.com/resend/2SHIfycCcJlAJEpt/images/audiences-intro-segment.png?fit=max&auto=format&n=2SHIfycCcJlAJEpt&q=85&s=550570d03d1b5611a89e5dddeadf79f9" alt="Segment" class="extraWidth" width="3736" height="1916" data-path="images/audiences-intro-segment.png" />

Learn more about [Segments](/docs/dashboard/segments/introduction).

## Topics

Topics are user-facing tools for managing email preferences. You can use them to manage your Contacts' email preferences.

<img src="https://mintcdn.com/resend/m2xttJpF68pi6Mw0/images/audience-topics-intro.png?fit=max&auto=format&n=m2xttJpF68pi6Mw0&q=85&s=0530a26f226771b486012abe36e9970a" alt="Topics" class="extraWidth" width="3024" height="1602" data-path="images/audience-topics-intro.png" />

When you send [Broadcasts](/docs/dashboard/broadcasts/introduction), you can optionally scope sending to a particular Topic. Not only does scoping your sending help you send more precisely, but it also allows your users to manage their preferences with more control.

<Tip>
  New to Topics? Learn [why and when to use
  them](/docs/knowledge-base/why-use-topics), including how they improve
  deliverability and differ from Segments.
</Tip>
