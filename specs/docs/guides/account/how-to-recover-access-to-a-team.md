> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to recover access to a team you can no longer sign in to

> How to get back into a Resend team when the email you signed in with no longer works or no admin is left on the team.

If the email you signed in with no longer works (e.g., a former employee's mailbox, a deleted Google account, an expired domain), or no admin is left on the team, use the case below that matches to recover team access:

* [An admin can still sign in](#an-admin-can-still-sign-in)
* [No admin can sign in](#no-admin-can-sign-in)
* [You only need the domain](#you-only-need-the-domain)

> [!NOTE]
>
> Support cannot change the email address on an existing login, so the fix is
> always to give a login you control access to the team.

## An admin can still sign in

An admin can fix your access without contacting support:

1. Signed in as an admin, go to [Team](https://resend.com/settings/team) and click **Invite**.
2. Enter an email address you control and choose the **Admin** role.
3. Accept the invite.

If you are already a member, an admin can change your role instead. See [Managing Teams](/docs/dashboard/settings/team.md).

> [!TIP]
>
> Always transfer admin access to another member if you foresee losing access to
> your email account. Invite the new admin from
> [Team](https://resend.com/settings/team), then leave the team.

## No admin can sign in

Support can restore access after you prove you own a domain on the team.

1. If you aren't a member of the team, sign up for a new Resend account with an address you control. If the old login used a Google account that no longer exists, sign up with email rather than Google.
2. [Contact support](https://resend.com/help). Include:
   * A domain that is on the team.
   * The email of the Resend account that should get access, and whether it's already a member of the team.
3. Support replies with a verification value that is unique to your request. Add a `TXT` record on that domain with the host `verification` and that value. The host must be exactly `verification`.
4. Reply to the support conversation with the name of the domain where you added the `TXT` record.

Once ownership is verified, support gives your account admin access to the team. Nothing on the team is changed, revoked or deleted in the process.

If you still control the old mailbox but the login asks for an MFA code you don't have access to, see our [Locked out by MFA](/docs/guides/account/locked-out-by-mfa.md) support article.

## You only need the domain

You can add the domain to a team you control and prove ownership with a self serve claim. See [Claiming a domain](/docs/dashboard/domains/claim.md). A claim moves the domain only and doesn't give you access to the old team. Safety checks can block a claim, for example when the domain was recently active on the other team.

Please [reach out to support](https://resend.com/help) for help with a domain claim.
