> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to add multi-factor authentication to your Resend account

> How to enable and disable multi-factor authentication (MFA) or two-factor authentication (2FA) on your Resend account, save your recovery code, and what to do if you lose your device.

Multi-factor authentication (MFA), also called two-factor authentication (2FA), adds an extra layer of security by requiring a second verification factor when you sign in.

## Enable MFA

To enable MFA on your Resend account:

1. Navigate to your [**Profile**](https://resend.com/profile) page.
2. Click **Enable MFA**.
3. Scan the QR code with your preferred authenticator app.
4. Enter the code provided by the authenticator app.
5. Copy the recovery code Resend shows you, store it, and click **I've saved my recovery code**.

Once MFA is enabled, you'll be asked for a code from your authenticator app whenever you sign in.

## Save your recovery code

If you lose access to your authenticator app, your recovery code turns off MFA so you can sign in and set it up again. The code works once, and Resend shows it only when you turn on MFA. Store it somewhere other than the device that holds your authenticator app, such as a password manager.

If you turned on MFA before recovery codes were introduced on 8 October 2026, your account has no recovery code yet. Generate one from your [**Profile**](https://resend.com/profile) page while you can still sign in.

## Disable MFA

To disable MFA on your Resend account:

1. Navigate to your [**Profile**](https://resend.com/profile) page.
2. Click **Revoke Access**.

After revoking access, you can sign in with your email and password without an authenticator code.

## If you change or lose your device

* **Changing phones:** while you can still sign in, click **Revoke Access** on your [**Profile**](https://resend.com/profile) page, then click **Enable MFA**, scan the new QR code with the authenticator app on your new device, and save the new recovery code.
* **Codes rejected:** use the entry your authenticator app created for Resend, not an entry for another service, and set your phone's clock to update automatically.
* **Device lost:** enter your recovery code when Resend asks for your authenticator code. MFA is turned off, you are signed in, and you can turn MFA on again with your new device. Without a recovery code, a password reset does not remove MFA, and another team member, including an admin, cannot reset it for you. Resend support can remove MFA after verifying that you own a domain on the account. See [Locked out by MFA: lost authenticator device](/docs/guides/account/locked-out-by-mfa.md) for the steps.

## MFA for your team

MFA is enabled per account, not per team. There is no setting to require or enforce MFA for everyone on your team. Each member enables it individually on their own [**Profile**](https://resend.com/profile) page.

Every member of the team can check who has enabled MFA from the [**Team Settings**](https://resend.com/settings/team) page. The **Enabled MFA** column is not admin-only. See [Managing Teams](/docs/dashboard/settings/team.md) for details.
