# Phishing Analysis

![Phishing Analysis](phishing-analysis.png)

## Overview

Phishing is one of the most common initial access techniques used by cybercriminals to steal credentials, distribute malware, or gain unauthorized access to an organization's systems. Security analysts must be able to investigate suspicious emails, identify Indicators of Compromise (IOCs), and determine whether an email is legitimate or malicious.

In this lab, I learned how email works, how phishing attacks are delivered, and how to analyze email headers, bodies, attachments, and embedded links to detect phishing attempts.

---

## Learning Objectives

- Understand how email communication works.
- Learn the structure of an email address.
- Understand SMTP, POP3, and IMAP.
- Analyze email headers.
- Investigate email bodies and HTML source.
- Analyze email attachments.
- Identify different phishing techniques.
- Detect Indicators of Compromise (IOCs).
- Safely investigate suspicious emails.

---

## Email Address Anatomy

*(ضع الصورة هنا)*

An email address consists of three primary components:

- **Username** – Identifies the recipient's mailbox.
- **@ Symbol** – Separates the user from the destination domain.
- **Domain Name** – Specifies the mail server responsible for receiving the message.

Example:

```
john@example.com
```

| Part | Description |
|------|-------------|
| john | Username |
| @ | Separator |
| example.com | Mail Domain |

---

## Email Delivery Process

*(ضع الصورة هنا)*

Emails travel through several protocols before reaching the recipient.

### SMTP (Simple Mail Transfer Protocol)

Used for:

- Sending emails
- Relaying mail between servers

---

### POP3 (Post Office Protocol)

Characteristics:

- Downloads emails locally.
- Usually removes emails from the server.
- Best for one device.

---

### IMAP (Internet Message Access Protocol)

Characteristics:

- Synchronizes emails across multiple devices.
- Messages remain stored on the server.
- Ideal for modern email clients.

---

## Email Delivery Workflow

*(ضع الصورة هنا)*

1. Sender writes an email.
2. SMTP sends it to the sender's mail server.
3. DNS locates the recipient's mail server.
4. The email is transferred across the Internet.
5. The recipient retrieves it using POP3 or IMAP.

---

## Email Body Analysis

*(ضع الصورة هنا)*

An email body may contain:

- Plain text
- HTML formatting
- Images
- Hyperlinks
- Embedded objects
- Attachments

HTML emails should always be inspected carefully because malicious content may be hidden behind legitimate-looking text.

---

## Viewing HTML Source

*(ضع الصورة هنا)*

Instead of only viewing the rendered email, analysts should inspect the raw HTML source to identify:

- Hidden hyperlinks
- Embedded images
- JavaScript (if present)
- Tracking pixels
- Obfuscated HTML

Analyzing the source code often reveals malicious elements that are invisible to the user.

---

## Attachment Analysis

*(ضع الصورة هنا)*

Email attachments are commonly used to deliver malware.

Important headers include:

| Header | Purpose |
|---------|----------|
| Content-Type | File type |
| Content-Disposition | Attachment name |
| Content-Transfer-Encoding | Encoding format |

Most attachments are encoded using **Base64**, allowing analysts to reconstruct and inspect the original file using tools such as:

- CyberChef
- Base64 Decoders
- Malware Sandboxes

---

# Types of Phishing

*(ضع الصورة هنا)*

## Spam

Bulk unsolicited emails sent to many recipients.

---

## Phishing

Attempts to impersonate trusted organizations and steal sensitive information.

---

## Spear Phishing

Highly targeted phishing directed at a specific person or organization.

---

## Whaling

Targets executives such as:

- CEO
- CFO
- Directors

Usually focuses on financial fraud.

---

## Smishing

Phishing delivered through SMS messages.

---

## Vishing

Voice-based phishing using phone calls.

---

# Anatomy of a Phishing Email

*(ضع الصورة هنا)*

Common phishing indicators include:

- Spoofed sender address
- Urgent language
- Fake branding
- Grammar mistakes
- Generic greetings
- Hidden hyperlinks
- Malicious attachments

These characteristics should always be investigated before interacting with the email.

---

## Safe Email Analysis

Never click suspicious links directly.

Instead, **Defang** them.

Example:

Original

```
http://malicious.com
```

Defanged

```
hxxp[://]malicious[.]com
```

Defanging prevents accidental execution while allowing safe investigation.

---

## Investigation Checklist

When analyzing a suspicious email, verify:

- Sender address
- Reply-To address
- Subject line
- Email headers
- Authentication results (SPF, DKIM, DMARC)
- URLs
- Attachments
- Writing style
- Indicators of Compromise (IOCs)

---

## Skills Gained

- Email Analysis
- Header Analysis
- HTML Inspection
- Attachment Analysis
- IOC Identification
- Social Engineering Detection
- Threat Hunting
- Incident Response
- Phishing Investigation

---

## Key Takeaways

- Email headers reveal the true origin of a message.
- HTML emails may hide malicious links.
- Attachments should always be analyzed before opening.
- Multiple phishing techniques target different victims.
- Defanging URLs prevents accidental interaction with malicious content.
- Proper email analysis helps prevent credential theft, malware infections, and unauthorized access.

---

## Conclusion

Phishing remains one of the primary initial access vectors used by attackers. Understanding email delivery, analyzing headers, inspecting HTML content, and recognizing phishing indicators are essential skills for SOC Analysts, Incident Responders, and Threat Hunters. These techniques help security teams quickly identify malicious emails, protect users, and strengthen organizational defenses against social engineering attacks.
