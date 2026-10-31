> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Security

> An overview of Resend security features and practices.

## Governance

Resend establishes policies and controls, monitors compliance with those controls, and proves the security and compliance to third-party auditors.

Our policies are based on the following **foundational principles**:

> [card] Least Privilege
>
> Access should be limited to only those with a legitimate business needs,
> based on the principle of least privilege.

> [card] Consistency
>
> Security controls should be applied consistently across all areas of the
> enterprise.

> [card] Defense in Depth
>
> Security controls should be implemented and layered according to the
> principle of defense-in-depth.

> [card] Continuous Improvement
>
> The implementation of controls should be iterative, continuously improving
> effectiveness and decreasing friction.

### Compliance Standards

> [accordion] SOC 2 Type II
>
> Resend is SOC 2 Type II compliant. The audit was completed by Vanta & Advantage Partners.
> You can download a copy of the report on the [Documents](https://resend.com/settings/documents) page.

> [accordion] GDPR
>
> Resend is GDPR compliant. You can learn more about our [GDPR compliance](https://resend.com/security/gdpr) or view our [DPA](https://resend.com/legal/dpa).

## Data Protection

> [card] Data at rest
>
> All datastores are encrypted at rest. Sensitive collections and tables also
> use row-level encryption.

> [card] Data in transit
>
> Resend uses TLS 1.3 or higher everywhere data is transmitted over
> potentially insecure networks.

> [card] Data backup
>
> Resend backs-up all production data using a point-in-time approach. Backups
> are persisted for 7 days.

## Product Security

### Penetration testing

Resend engages with third-party firms to conduct penetration testing at least annually.

All areas of the Resend product and cloud infrastructure are in-scope for these assessments, and source code is fully available to the testers to maximize the effectiveness and coverage.

You can download the latest penetration test report on the [Documents](https://resend.com/settings/documents) page.

### Vulnerability scanning

Resend uses multiple vulnerability monitoring techniques including code-level scanning, dependency scanning, and security reviews to identify and remediate vulnerabilities.

Vulnerabilities are prioritized based on severity and risk, and are remediated according to the following schedule:

* Critical: 15 Days
* High: 30 Days
* Medium: 90 Day
* Low: 180 Days
* Informational: As needed

## Enterprise Security

> [card] Endpoint protection
>
> All company devices are equipped with anti-malware protection. Endpoint security alerts are monitored with 24/7/365 coverage. We use MDM software to enforce secure configuration of endpoints, such as disk encryption, screen lock configuration, and software updates.

> [card] Security education
>
> Resend provides comprehensive security training to all employees upon onboarding and annually.
>
> Resend's conducts threat briefings with employees to inform them of important security and safety-related updates that require special attention or action.

> [card] Identity and access management
>
> Resend employees are granted access to applications based on their role, and automatically deprovisioned upon termination of their employment. Further access must be approved according to the policies set for each application.
>
> Multi-factor authentication is required for all employees to access company applications.

## Responsible Disclosure

To report a vulnerability, please check the guidelines on the [Responsible Disclosure](https://resend.com/security/responsible-disclosure) page.
