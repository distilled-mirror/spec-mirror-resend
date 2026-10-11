> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Locked out by MFA

> How to use your MFA recovery code when you lose your authenticator app, and how Resend support verifies ownership when you have no recovery code.

If you turned on multi factor authentication (MFA) and can no longer get a code from your authenticator app, use your recovery code to turn MFA off and sign in. If you don't have a recovery code, Resend support can remove MFA from your login after verifying that you own the account.

## Check the code first

If your authenticator app still has a Resend entry but the codes are rejected:

* Use the entry your authenticator app created when you turned on MFA in Resend.
* Set your phone's clock to update automatically. A phone clock that is off produces codes that don't match.

## Reset MFA with your recovery code

Your recovery code is the single code Resend showed when you turned on MFA. It has ten characters split by a dash, in the format `XXXXX-XXXXX`.

<Steps>
  <Step title="Turn off MFA with your recovery code">
    Using your recovery code turns off MFA and allows you to sign in with your usual method.

    <Info>
      If you also lost access to the email address you sign in with, see our
      [recover access to a team](/docs/guides/account/how-to-recover-access-to-a-team)
      support article.
    </Info>

    To use your recovery code, sign in with your usual method and enter your recovery code when Resend asks for your authenticator code. ([View help](#if-you-do-not-have-a-recovery-code) if you do not have a recovery code.)

    The recovery code works once. Using it also:

    * Signs out every other active session on your account.
    * Sends an email titled "Your Resend two-factor authentication was reset" to your email address.

    Removing MFA only removes the authenticator factor. The domains and API keys on the account stay untouched.
  </Step>

  <Step title="Turn on MFA again">
    Enable MFA on again from your [Profile](https://resend.com/profile) with your new device. Resend shows you a new recovery code when you do. Save it before you close the dialog. See [how to add MFA](/docs/knowledge-base/how-can-i-add-mfa) for more details.

    If you receive that email and did not use your recovery code, reset your password and [contact support](https://resend.com/help) immediately.
  </Step>
</Steps>

## MFC recovery code security

Resend shows the recovery code once, when you turn on MFA, and does not show it again. Copy it and store it somewhere other than the device that holds your authenticator app, such as a password manager.

## What does not remove MFA

* **A password reset.** After the reset, sign in still asks for the authenticator code.
* **Another team member.** MFA belongs to each login, not to the team. Another member, including an admin, cannot reset or disable it for you.

## If you do not have a recovery code

You can ask support to remove MFA for you.

1. Contact support from [Help](https://resend.com/help). In your first message, include:
   * The email address you sign in with.
   * A domain that is already on the account.
   * A note if you never turned on MFA yourself, so support can review the account before anything changes.

2. Support will reply with a verification value that is unique to your request. Add it as a DNS record on that domain to prove you own it:

   | Host | Type | Value |
   | - | - | - |
   | `verification` | `TXT` | The value from support |

   Most DNS providers display this record as `verification.yourdomain.com`. The host must be exactly `verification`.

3. Once the record is in place, reply the support conversation and name the domain with the verification record.

If there are no domains on the account, communicate with Support to verify ownership another way.
