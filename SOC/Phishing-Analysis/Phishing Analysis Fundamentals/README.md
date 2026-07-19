# Phishing Analysis

![Email Address](Email%20Address.png)

## Introduction

Spam and phishing remain among the most common social engineering threats facing modern organizations. While spam is often low-risk, phishing emails are specifically designed to steal credentials, deliver malware, or trick users into revealing sensitive information. A single click on a malicious attachment or fake login page can provide an attacker with an initial foothold inside a company's network.

As a Security Analyst or SOC Analyst, analyzing suspicious emails is one of the most important daily tasks. By examining email headers, message content, links, and attachments, defenders can identify malicious campaigns, block future attacks, and improve an organization's security posture.

### Learning Objectives

- Understand how email communication works.
- Learn the structure of an email address.
- Understand SMTP, POP3, and IMAP.
- Analyze email headers.
- Investigate email bodies and HTML source.
- Understand different phishing techniques.
- Learn how to safely analyze suspicious emails.

---

![Email Delivery](Email%20Delivery.png)

# Email Delivery

Email communication depends on three primary protocols:

- **SMTP (Simple Mail Transfer Protocol):** Responsible for sending emails.
- **POP3 (Post Office Protocol):** Downloads emails to a single device.
- **IMAP (Internet Message Access Protocol):** Synchronizes emails across multiple devices while keeping them stored on the server.

### POP3

- Downloads emails locally.
- Usually removes emails from the server.
- Best suited for one device.

### IMAP

- Keeps emails on the mail server.
- Synchronizes multiple devices.
- Recommended for modern email services.

### Email Journey

1. User sends an email.
2. SMTP transfers it to the sender's mail server.
3. DNS finds the recipient's mail server.
4. The email is delivered.
5. Recipient retrieves it using POP3 or IMAP.

---

![Email Headers](Email%20Headers.png)

# Email Headers

Email headers contain valuable metadata that can help identify phishing attempts.

Important header fields include:

- **From:** Claimed sender.
- **To:** Recipient.
- **Subject:** Email title.
- **Date:** Time sent.
- **Return-Path:** Actual return address.
- **Received:** Mail server path.
- **Message-ID:** Unique identifier.
- **Reply-To:** Address used when replying.

Security analysts often examine these headers to identify spoofing attempts and trace the real sender.

---

![Viewing the Message Source](Viewing%20the%20Message%20Source.png)

# Viewing the Message Source

Viewing the raw email source allows analysts to inspect:

- Complete email headers.
- MIME structure.
- HTML code.
- Attachments.
- Hidden URLs.
- Encoding methods.

This provides much more information than simply reading the email inside an email client.

---

![Email Body](Email%20Body.png)

# Email Body

The email body contains the message presented to the recipient.

It may be:

- Plain Text
- HTML

HTML emails can include:

- Images
- Hyperlinks
- Buttons
- Styling
- Embedded content

Attackers frequently abuse HTML formatting to hide malicious links behind legitimate-looking buttons.

---

![Viewing HTML Source Code](Viewing%20HTML%20Source%20Code.png)

# Viewing HTML Source Code

Inspecting the HTML source allows analysts to:

- Reveal hidden links.
- Inspect embedded images.
- Find suspicious JavaScript.
- Detect phishing forms.
- Verify actual URLs.

Comparing the rendered email with its HTML source often exposes malicious elements invisible to normal users.

---

![Reconstructing Attachments](Reconstructing%20Attachments.png)

# Reconstructing Attachments

Attachments are embedded using MIME encoding.

Useful fields include:

- **Content-Type:** File type.
- **Content-Disposition:** Indicates attachment and filename.
- **Content-Transfer-Encoding:** Usually Base64.

Base64 data can be decoded using tools such as:

- CyberChef
- Base64 Decoders

This allows analysts to reconstruct and safely inspect suspicious files.

---

![Anatomy of a Phishing Email](Anatomy%20of%20a%20Phishing%20Email.png)

# Types of Phishing

Common phishing attacks include:

- Spam
- Phishing
- Spear Phishing
- Whaling
- Smishing
- Vishing

## Common Indicators of Phishing Emails

- Spoofed sender address.
- Urgent language.
- Brand impersonation.
- Grammar or spelling mistakes.
- Generic greetings.
- Hidden or shortened URLs.
- Malicious attachments.

## Safe Analysis

Never click suspicious links directly.

Always **defang** indicators before sharing them.

Example:

Original:
