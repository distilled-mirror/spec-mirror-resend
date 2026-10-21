> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Can I merge accounts or teams?

> Teams cannot be merged, but you can move people, domains and your plan onto the one team you want to keep.

No, teams can't be merged. Each team has its own API keys, billing, and usage, and API keys. Email history and plans can't be moved from one team to another. To consolidate teams, pick the team you want to keep and move people and domains into it.

> [!NOTE]
>
> Email history stays with the team it was sent from. Before you delete a team,
> an admin can download emails, logs, domains, contacts, and other data as CSV
> with the **Export** button on those pages.

## Consolidate onto one team

**1. Choose the team to keep**

If it needs a paid plan, select that team and upgrade it from
[Billing](https://resend.com/settings/billing).

**2. Invite your teammates**

In [Team](https://resend.com/settings/team), click **Invite**, enter each
person's email address and choose **Admin** or **Member**. Those with access
to additional accounts can switch between teams using the switcher in the
top left corner.

**3. Move each domain**

Delete each domain in the old team and re-add each domain to the team you
want to keep. Deleting a domain can't be undone.

**4. Create new API keys**

Once your domains are verified on the kept team, create keys from [API
keys](https://resend.com/api-keys) and update your applications.

**5. Retire the old teams**

Cancel any plan on the teams you no longer need. Then delete each team from
[the team settings](https://resend.com/settings/team). Deleting the team
removes all its data and isn't reversible. For more help, see [How to delete
your Resend team](/docs/knowledge-base/how-can-i-delete-my-team).

## If you can no longer reach the other team

If a domain sits on a team you no longer have access to, add the domain on the team you want to keep. Resend will prompt you to start a claim, which proves ownership with a TXT record. See [Claiming a domain](/docs/dashboard/domains/claim) for more information.

## Several products or clients in one team

One team can serve several products or clients. See the [multi tenant setup guide](/docs/knowledge-base/setting-up-resend-for-multi-tenants) for recommended setup.

## Additional support

If a domain claim is blocked or you are unsure which team to keep, contact [Resend support](https://resend.com/help) for assistance.
