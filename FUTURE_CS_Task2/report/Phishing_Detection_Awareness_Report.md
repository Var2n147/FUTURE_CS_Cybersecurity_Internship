# Phishing Detection & Awareness Report

## Future Interns Cybersecurity Internship – Task 2

**Project:** Phishing Email Detection & Awareness System  
**Task ID:** FUTURE_CS_02  
**Prepared by:** Varun Pant  
**Date:** 2 October 2026

---

# 1. Executive Summary

Phishing is a social-engineering attack in which an attacker attempts to
deceive a recipient into revealing sensitive information, opening
malicious content, or visiting a fraudulent website.

This assessment analyzes three phishing email examples and identifies
the characteristics that can help users recognize phishing attacks.

The analysis focuses on sender identity, social-engineering techniques,
suspicious links or attachments, urgency, impersonation, and the potential
for credential theft.

The three analyzed examples were classified as phishing based on the
available evidence.

---

# 2. Objective

The objectives of this assessment are:

- Analyze phishing email examples.
- Identify common phishing indicators.
- Classify email risk as Safe, Suspicious, or Phishing.
- Explain phishing attacks in simple language.
- Develop practical employee awareness guidance.
- Recommend safe actions for users who receive suspicious messages.

---

# 3. Scope

The assessment covers:

1. Sender and impersonation indicators.
2. Email subject and message content.
3. Social-engineering techniques.
4. Suspicious URLs.
5. Unexpected attachments.
6. Email-header availability.
7. Risk classification.
8. User prevention and awareness.

The analysis does not intentionally open potentially malicious URLs or
attachments.

---

# 4. Methodology

The following workflow was used:

```text
Sample Collection
       ↓
Sample Sanitization
       ↓
Sender & Content Examination
       ↓
URL / Attachment Examination
       ↓
Header Availability Check
       ↓
Phishing Indicator Identification
       ↓
Risk Classification
       ↓
Attack Explanation
       ↓
Prevention Recommendations
```

Public phishing examples were used for educational analysis. Third-party
content was not claimed as original work.

---

# 5. Risk Classification Method

## Safe

No significant phishing indicators are identified from the available
evidence.

## Suspicious

One or more unusual characteristics are present, but available evidence
is insufficient for a confident phishing classification.

## Phishing

Multiple indicators strongly support a fraudulent or credential-harvesting
attempt.

---

# 6. Sample 01 – Account Lockout

## Source

Educational sample supplied directly in the Future Interns Task 2
description.

## Classification

**PHISHING – HIGH CONFIDENCE**

## Indicators

- Urgent account-lockout subject.
- Fear-based language.
- 24-hour deadline.
- Generic greeting.
- Suspicious account-verification domain.
- Request to verify account details through an unexpected link.

## Attack Explanation

The message attempts to make the recipient afraid of losing account access.
The user is then encouraged to follow a verification link.

A fraudulent destination could potentially request credentials or other
sensitive information.

The destination was not opened during this analysis.

## User Recommendation

Do not click the link. Open the organization's official website directly
or contact the organization's support team through a trusted channel.

---

# 7. Sample 02 – Password Expiration

## Source

SeanWrightSec/phishing-examples public educational repository.

## Classification

**PHISHING – HIGH CONFIDENCE**

## Indicators

- IT-department impersonation.
- Password-expiration theme.
- Urgency.
- Suspicious password-update link.
- Potential credential-harvesting objective.

## Attack Explanation

The attacker attempts to convince the recipient that their password needs
immediate attention.

The victim may follow the supplied link and enter credentials into a
fraudulent login page.

The linked destination was not intentionally opened during this analysis.

## User Recommendation

Do not use the email link to update the password. Open the organization's
known account portal directly and verify the password status there.

---

# 8. Sample 03 – App Store Purchase

## Source

SeanWrightSec/phishing-examples public educational repository.

## Classification

**PHISHING – HIGH CONFIDENCE**

## Indicators

- Trusted-brand impersonation.
- Unexpected purchase notification.
- Concern about unauthorized financial activity.
- Unexpected PDF attachment.
- Social-engineering pressure.

## Attack Explanation

The attacker uses a familiar brand and a supposed purchase to create
concern.

The recipient may open the attachment or follow instructions provided by
the message.

The attachment was not opened during this educational analysis.

## User Recommendation

Do not open unexpected attachments. Verify the transaction directly
through the official application or website.

---

# 9. Comparative Findings

| Indicator | Sample 01 | Sample 02 | Sample 03 |
|---|---|---|---|
| Urgency | Yes | Yes | Indirect |
| Fear/Concern | Yes | Yes | Yes |
| Brand/Organization Impersonation | Yes | Yes | Yes |
| Suspicious Link | Yes | Yes | Not primary |
| Unexpected Attachment | No | No | Yes |
| Social Engineering | Yes | Yes | Yes |
| Credential Theft Risk | High | High | Possible |
| Classification | Phishing | Phishing | Phishing |

---

# 10. Common Phishing Indicators

## 10.1 Unexpected Urgency

Attackers frequently create deadlines to prevent users from thinking
carefully.

Examples include:

- Account will be locked.
- Password expires today.
- Payment must be confirmed immediately.
- Security verification required within 24 hours.

Users should slow down and independently verify the request.

## 10.2 Fear and Threats

Messages may threaten account suspension, financial loss, or security
problems.

Users should not allow fear or urgency to replace normal verification
procedures.

## 10.3 Suspicious Sender

Users should check the complete email address instead of trusting only
the display name.

A familiar display name does not prove that the message came from the
organization.

## 10.4 Suspicious Links

A link may lead to a domain unrelated to the organization it claims to
represent.

Users should avoid opening unexpected links and instead navigate to the
official website independently.

## 10.5 Unexpected Attachments

Unexpected PDFs, documents, archives, or executable files can be used to
deliver malicious content or direct users toward fraudulent websites.

## 10.6 Generic Greetings

Messages such as "Dear User" can be suspicious when a legitimate service
normally knows the customer's identity.

A generic greeting alone does not prove phishing, but it can contribute
to the overall assessment.

## 10.7 Requests for Credentials or OTPs

Requests for passwords, one-time passwords, authentication codes, or other
sensitive information should be treated with caution.

Legitimate organizations generally have established secure methods for
authentication and account management.

---

# 11. How a Typical Phishing Attack Works

A simplified phishing attack can follow this process:

```text
Attacker creates deceptive message
              ↓
Message impersonates trusted organization
              ↓
Victim receives message
              ↓
Urgency / fear / curiosity is created
              ↓
Victim clicks link or opens attachment
              ↓
Fake website / malicious content
              ↓
Credentials or sensitive information may be exposed
```

The exact behavior depends on the attack and should not be assumed from
the email alone.

---

# 12. Employee Awareness Guidelines

## DO

- Verify the sender's complete email address.
- Check suspicious links before opening them.
- Navigate to important services using a known official website or
  application.
- Verify unexpected payment requests using another communication channel.
- Report suspicious emails to IT/security.
- Treat unexpected attachments cautiously.
- Use multi-factor authentication where available.
- Ask the security team when uncertain.
- Confirm unusual requests involving passwords or financial information.

## DON'T

- Do not click unexpected links.
- Do not enter passwords after following suspicious email links.
- Do not share OTPs or authentication codes.
- Do not open unexpected attachments.
- Do not reply to suspicious messages.
- Do not allow urgency to override verification procedures.
- Do not trust a message only because it uses a familiar company logo.
- Do not assume HTTPS alone means a website is legitimate.
- Do not download files simply because an email claims they are important.

---

# 13. What To Do If You Clicked a Phishing Link

If a user accidentally clicks a suspicious link:

1. Stop interacting with the page.
2. Do not enter credentials or sensitive information.
3. Close the suspicious page.
4. Report the incident to IT/security.
5. If credentials were entered, change the password through the official
   website.
6. Review account activity for suspicious behavior.
7. Follow the organization's incident-response procedure.

If sensitive information was submitted, the incident should be reported
promptly rather than hidden.

---

# 14. Header Analysis

Email headers can provide useful information about message routing and
authentication.

Relevant fields may include:

- From
- Reply-To
- Return-Path
- Received
- Message-ID
- Authentication-Results
- SPF
- DKIM
- DMARC

For this project, the sanitized versions of Samples 02 and 03 did not
include complete raw headers.

Therefore, authentication results and originating infrastructure were
not fabricated.

For a real investigation, analysts should obtain the complete original
message headers and analyze them with an appropriate header-analysis tool.

---

# 15. URL and Attachment Safety

Potentially malicious URLs and attachments were not intentionally opened
during this assessment.

Suspicious URLs should be represented in defanged form when included in
documentation, for example:

```text
http://example[.]com
```

instead of:

```text
http://example.com
```

This reduces the chance of accidental navigation.

Similarly, suspicious attachments should not be opened on a normal
personal system. If deeper analysis is required, security analysts should
use an isolated analysis environment according to organizational policy.

---

# 16. Limitations

This assessment has several limitations:

1. The first sample is an educational example rather than a captured
   mailbox message.
2. Samples 02 and 03 are sanitized descriptions of public educational
   examples.
3. Complete raw headers were not available for all samples.
4. Potentially malicious URLs and attachments were not intentionally
   opened.
5. Classification is based on the evidence available in the samples.
6. No claim is made that the public samples were originally collected by
   the author of this report.

These limitations are documented so that the report does not claim
evidence that was not actually observed.

---

# 17. Recommendations for Organizations

Organizations should:

- Provide regular phishing-awareness training.
- Enable strong email authentication controls.
- Use email filtering and anti-phishing protections.
- Provide an easy phishing-reporting mechanism.
- Encourage users to report mistakes without fear of punishment.
- Use multi-factor authentication.
- Establish procedures for suspicious payment and credential requests.
- Conduct controlled security-awareness exercises.
- Monitor reported phishing messages and recurring attack patterns.
- Maintain an incident-response procedure for suspected phishing attacks.

---

# 18. Practical Employee Checklist

Before interacting with an unexpected email, ask:

### STOP

**S – Stop and do not react immediately.**

**T – Think about whether you expected the message.**

**O – Observe the sender, links, attachments, and wording.**

**P – Proceed only after independently verifying the request.**

If anything appears suspicious, report the message to the appropriate
security or IT team.

---

# 19. Conclusion

The assessment demonstrates how phishing attacks commonly combine
impersonation, urgency, fear, suspicious links, unexpected attachments,
and trusted-brand references.

The most important defensive behavior is to slow down and independently
verify unexpected requests.

Users should never assume that an email is legitimate simply because it
contains familiar branding or appears urgent.

Phishing awareness is therefore an important part of organizational
security because a well-informed user can prevent an attack before it
progresses to credential theft or other compromise.

---

# 20. References

1. Future Interns – Cyber Security Task 2 (2026)
2. SeanWrightSec – phishing-examples
3. rf-peixoto – phishing_pot
4. Google Admin Toolbox – Messageheader
5. Google Gmail Help – Trace an email with its full header

See `../references/sources.md` for the source details and URLs.
