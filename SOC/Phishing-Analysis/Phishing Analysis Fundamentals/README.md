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
- Investigate email bodies.
- Analyze HTML source code.
- Analyze email attachments.
- Identify different phishing techniques.
- Detect Indicators of Compromise (IOCs).
- Safely investigate suspicious emails.

---

# Email Address Anatomy

![Email Address](Email%20Address.png)

Every email begins with an email address, and understanding its structure is essential when analyzing phishing emails.

An email address consists of three main components:

- **Username** – Identifies the recipient's mailbox.
- **@ Symbol** – Separates the username from the destination domain.
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

A spoofed domain such as **micr0soft.com** instead of **microsoft.com** is a common phishing indicator.

---

# Email Delivery

![Email Delivery](Email%20Delivery.png)

Email communication relies on three primary protocols.

## SMTP (Simple Mail Transfer Protocol)

Responsible for:

- Sending emails
- Relaying emails between mail servers

---

## POP3 (Post Office Protocol)

Characteristics:

- Downloads emails to one device.
- Emails are often removed from the server.
- Best suited for a single device.

---

## IMAP (Internet Message Access Protocol)

Characteristics:

- Synchronizes emails across multiple devices.
- Keeps emails stored on the server.
- Allows consistent access from different devices.

---

## Email Journey

![Email Headers](Email%20Headers.png)

The email delivery process follows these steps:

1. User sends an email.
2. SMTP transfers the message to the sender's mail server.
3. DNS locates the recipient's mail server.
4. The email is delivered across the Internet.
5. The recipient retrieves it using POP3 or IMAP.

Understanding this workflow helps analysts trace the origin of suspicious emails.

---

# Email Body Analysis

![Email Body](Email%20Body.png)

The email body contains the visible content received by the user.

Emails may be:

- Plain Text
- HTML
- Rich formatted messages

HTML emails can contain:

- Images
- Hyperlinks
- Buttons
- Embedded content
- Tracking pixels

Attackers frequently abuse HTML formatting to disguise malicious content.

---

# Viewing HTML Source

![Viewing HTML Source Code](Viewing%20HTML%20Source%20Code.png)

Email clients display the rendered version of an email, but analysts should always inspect the raw HTML source.

Viewing the HTML source helps identify:

- Hidden hyperlinks
- Embedded images
- Suspicious HTML tags
- Obfuscated code
- Tracking elements

---

## Viewing the Message Source

![Viewing the Message Source](Viewing%20the%20Message%20Source.png)

Viewing the complete message source provides access to:

- Email Headers
- MIME structure
- HTML source
- Attachments
- Content encoding

This information is invaluable during phishing investigations.

---

# Attachment Analysis

![Reconstructing Attachments](Reconstructing%20Attachments.png)

Attachments are one of the most common malware delivery methods.

Important attachment headers include:

| Header | Description |
|---------|-------------|
| Content-Type | File type |
| Content-Disposition | Attachment name |
| Content-Transfer-Encoding | Encoding method |

Most attachments are Base64 encoded and can be reconstructed using tools such as:

- CyberChef
- Base64 Decoders
- Malware Sandboxes

Always analyze attachments inside a secure environment.

---

# Types of Phishing

Attackers use several phishing techniques depending on their target.

## Spam

Mass unsolicited emails.

---

## Phishing

Attempts to steal sensitive information by impersonating trusted organizations.

---

## Spear Phishing

Highly targeted phishing against specific individuals or organizations.

---

## Whaling

Targets executives such as:

- CEO
- CFO
- Directors

Usually intended for financial fraud.

---

## Smishing

Phishing delivered via SMS messages.

---

## Vishing

Voice-based phishing using telephone calls.

---

# Anatomy of a Phishing Email

![Anatomy of a Phishing Email](Anatomy%20of%20a%20Phishing%20Email.png)

Common phishing characteristics include:

- Spoofed sender address
- Urgent subject lines
- Brand impersonation
- Generic greetings
- Grammar or spelling mistakes
- Hidden or shortened URLs
- Malicious attachments

SOC analysts should verify each of these indicators before determining whether an email is malicious.

---

# Safe Email Analysis

Never click suspicious links directly.

Instead, **Defang** them.

Original URL

```
http://malicious-domain.com
```

Defanged URL

```
hxxp[://]malicious-domain[.]com
```

Defanging prevents accidental interaction with malicious websites while allowing analysts to safely share indicators.

---

# Investigation Checklist

During every phishing investigation, verify:

- Sender address
- Reply-To address
- Return-Path
- Subject line
- Email headers
- SPF
- DKIM
- DMARC
- URLs
- Attachments
- HTML source
- Indicators of Compromise (IOCs)

---

# Skills Gained

- Email Analysis
- Email Header Analysis
- HTML Source Inspection
- Attachment Analysis
- IOC Identification
- Phishing Investigation
- Threat Hunting
- Incident Response
- Social Engineering Detection

---

# Key Takeaways

- Email headers reveal the true origin of a message.
- SMTP, POP3, and IMAP each serve different roles in email communication.
- HTML emails may hide malicious content.
- Attachments should always be analyzed safely.
- Defanging protects analysts from accidental interaction.
- Phishing emails often rely on urgency, impersonation, and social engineering rather than technical exploits.
- Proper email analysis significantly reduces the risk of credential theft and malware infections.

---

# Conclusion

Phishing remains one of the most effective initial access techniques used by attackers. Understanding how email works, analyzing headers, inspecting HTML content, examining attachments, and recognizing phishing indicators are fundamental skills for SOC Analysts, Incident Responders, and Threat Hunters.

By mastering these techniques, defenders can quickly identify malicious emails, protect users, and strengthen an organization's overall security posture against social engineering attacks.
