# Sample 01 – Phishing Analysis

## 1. Sample Information

| Field | Value |
|---|---|
| Sample ID | FUTURE-CS-T2-001 |
| Source | Future Interns educational task example |
| Email Type | Account verification / account suspension |
| Classification | Phishing |
| Confidence | High |

## 2. Subject Analysis

**Subject:** Urgent: Your Account Will Be Locked

The subject creates urgency and fear by suggesting that the recipient's
account will be locked. This is a common social-engineering technique
used to encourage users to act without carefully verifying the message.

## 3. Sender Analysis

The displayed sender is:

`Security Team <security@example.com>`

The message does not provide a verifiable organizational identity.
A legitimate security notification should normally be verified through
the organization's known communication channels.

## 4. Phishing Indicators

### Indicator 1 – Urgency

The email asks the user to verify the account immediately and provides
a 24-hour deadline.

### Indicator 2 – Fear-Based Language

The message threatens permanent account lockout if the recipient does
not comply.

### Indicator 3 – Generic Greeting

The message begins with:

`Dear User`

rather than identifying the recipient by name.

### Indicator 4 – Suspicious URL

The message contains:

`http://secure-account-verify[.]com`

The domain appears generic and is not clearly associated with a known
organization.

### Indicator 5 – Request for Verification

The recipient is instructed to follow a link and verify account details.
This can be used to direct victims toward a credential-harvesting page.

## 5. Header Analysis

No complete raw email headers were provided with this educational
sample.

Therefore, SPF, DKIM, DMARC, originating IP, and mail-routing information
cannot be independently verified for this sample.

These values are intentionally not assumed or fabricated.

## 6. Risk Classification

**Classification: PHISHING**

### Reason

The sample contains multiple strong phishing indicators:

- Urgent account-lockout threat
- Fear-based language
- Generic greeting
- Suspicious domain
- Request to verify account information through a link

Taken together, these indicators strongly support a phishing
classification.

## 7. How the Attack Could Work

A potential attack flow would be:

1. The attacker sends an email claiming to be a security team.
2. The email creates urgency by threatening account suspension.
3. The victim clicks the verification link.
4. The link could lead to a fraudulent website.
5. The fraudulent website could attempt to collect credentials or other
   sensitive information.

The exact behavior of the linked website has not been tested because the
URL has intentionally not been opened.

## 8. Recommended User Action

A user receiving this message should:

- Avoid clicking the link.
- Avoid entering passwords or other sensitive information.
- Verify the account through the organization's official website or
  application.
- Report the message to the organization's security/IT team.
- Delete or quarantine the message according to organizational policy.

## 9. Conclusion

The email demonstrates several common phishing techniques, particularly
urgency, fear, generic addressing, and a suspicious account-verification
link. Users should independently verify account-security messages instead
of following unexpected links.
