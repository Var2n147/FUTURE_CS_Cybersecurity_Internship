# Sample 03 – Apple App Store Purchase Phishing

## 1. Sample Information

| Field | Value |
|---|---|
| Sample ID | FUTURE-CS-T2-003 |
| Source | SeanWrightSec/phishing-examples |
| Category | Brand impersonation |
| Classification | Phishing |
| Confidence | High |

## 2. Attack Theme

The message impersonates Apple/App Store communications and presents the
recipient with information about a supposed purchase.

The purpose is to create concern about an unfamiliar transaction and
encourage the recipient to interact with the message.

## 3. Phishing Indicators

### 3.1 Trusted-Brand Impersonation

The message uses the identity of a familiar technology brand to create
trust.

### 3.2 Unexpected Purchase Notification

An unfamiliar purchase can cause the recipient to react quickly because
they may believe their account or payment method has been compromised.

### 3.3 Unexpected Attachment

The message attempts to direct the recipient toward an attached PDF.
Unexpected attachments should be treated cautiously.

### 3.4 Social Engineering

The message relies on curiosity and concern about a financial transaction
to encourage interaction.

## 4. Header Analysis

The sanitized educational sample available for this project does not
provide a complete raw header.

Therefore:

- SPF: Not available
- DKIM: Not available
- DMARC: Not available
- Originating IP: Not available
- Complete routing information: Not available

No authentication results are invented.

## 5. Risk Classification

**PHISHING – HIGH CONFIDENCE**

The combination of brand impersonation, an unexpected purchase notification,
and an unexpected attachment strongly indicates a phishing attempt.

## 6. How the Attack Could Work

1. An attacker sends a message impersonating a trusted brand.
2. The message claims that a purchase has occurred.
3. The recipient becomes concerned about unauthorized activity.
4. The recipient opens the attachment or follows instructions in the
   message.
5. The attachment or subsequent interaction could be used to steal
   information or redirect the victim to a malicious destination.

The attachment was not opened during this educational analysis.

## 7. Recommended User Response

Users should:

- Avoid opening unexpected attachments.
- Check purchases through the official application or website.
- Avoid using contact details supplied only in a suspicious email.
- Report suspicious messages to the organization's security team.
- Delete or quarantine the message according to security policy.

## 8. Conclusion

Attackers can exploit trust in well-known brands and concern about
unexpected purchases. Users should independently verify transactions
through official applications or websites rather than interacting with
unexpected email attachments.
