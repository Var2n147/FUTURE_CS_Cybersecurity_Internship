# Sample 02 – Microsoft Password Expiration Phishing

## 1. Sample Information

| Field | Value |
|---|---|
| Sample ID | FUTURE-CS-T2-002 |
| Source | SeanWrightSec/phishing-examples |
| Category | Credential phishing |
| Classification | Phishing |
| Confidence | High |

## 2. Attack Theme

The email impersonates an organization's IT department and claims that
the recipient's password has expired or requires immediate updating.

The objective is to persuade the recipient to click a password-update
link.

## 3. Phishing Indicators

### 3.1 Impersonation

The message presents itself as an organizational IT/security message.
This attempts to make the request appear trustworthy.

### 3.2 Account/Password Pressure

Password expiration creates concern that the user could lose access to
their account.

### 3.3 Urgency

The recipient is encouraged to take action quickly instead of independently
checking the request.

### 3.4 Suspicious Link

The password-update destination does not correspond to the legitimate
organization's expected domain.

### 3.5 Credential Harvesting Risk

A fraudulent password-update page could be used to collect usernames,
passwords, or other authentication information.

## 4. Header Analysis

The sanitized sample used for this project does not contain a complete
raw email header.

Therefore:

- SPF: Not available
- DKIM: Not available
- DMARC: Not available
- Originating IP: Not available
- Complete mail-routing path: Not available

These values are not assumed or fabricated.

## 5. Risk Classification

**PHISHING – HIGH CONFIDENCE**

The combination of organizational impersonation, password-related
urgency, and a suspicious password-update link strongly supports the
classification.

## 6. How the Attack Could Work

1. An attacker sends an email pretending to be organizational IT.
2. The message claims that the user's password needs immediate action.
3. The victim follows the supplied link.
4. The link may lead to a fraudulent login or password-update page.
5. Credentials entered on that page could be collected by the attacker.

The linked destination was not intentionally opened during this analysis.

## 7. Recommended User Response

Users should:

- Avoid clicking the supplied link.
- Open the organization's known website directly.
- Check the password status through the normal account portal.
- Contact IT/security if the message is unexpected.
- Report the email according to organizational procedures.

## 8. Conclusion

Password-expiration messages are effective phishing lures because they
combine a familiar business process with urgency. Users should verify
password-related requests through trusted channels instead of following
unexpected email links.
