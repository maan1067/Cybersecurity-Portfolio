# Phishing Emails in Action

## Introduction

In the first room of the **Phishing Analysis** module, **Phishing Analysis Fundamentals**, you learned how to investigate email headers and bodies to identify common red flags. Now, we transition to practice by examining real phishing email samples.

This room focuses on the tactics attackers use to mirror legitimate communications. By analyzing real samples, you will learn to identify the subtle nuances that distinguish a routine notification from a sophisticated credential harvesting attempt.

> **Note:** The samples throughout this room contain information from actual emails. Proceed with caution if you attempt to interact with any IP, domain, or attachment.

### Objectives

- Identify common social engineering tactics used in phishing.
- Analyze red flags contained within phishing emails.
- Detect link manipulation and tracking pixels.
- Deconstruct credential harvesting and attachment manipulation.

### Prerequisites

Complete **Phishing Analysis Fundamentals** for an overview of email communications and analysis.

---

# Cancel Your Order

In this task, we will examine a sample email designed to mimic an official transaction receipt from **PayPal**.

By analyzing this phishing email, we will focus on how attackers leverage spoofed email addresses to impersonate trusted services and use URL shortening services to hide the true destination of malicious links.

---

## Phishing Techniques Used

The phishing email uses several social engineering techniques:

- **Spoofed Email Address:** Mimicking a trusted service to gain immediate credibility.
- **URL Shortening:** Using redirect services to hide the true destination of a malicious link.
- **Branded HTML:** Impersonating PayPal branding to make the email appear legitimate.

---

## First Observations

Let's first examine the email header and identify immediate warning signs.

### Subject Line

The attacker uses a fake purchase confirmation to create urgency and pressure the victim into reacting quickly.

### From Address

Although the sender appears to be:

```
service@paypal.com
```

the actual email originates from:

```
gibberish@sultanbogor.com
```

This mismatch is an immediate indicator of sender spoofing.

### To Address

The recipient address is also unusual and does not resemble a normal Yahoo email account, adding another red flag.

---

## Email Body Analysis

The email body is carefully designed to resemble a legitimate PayPal receipt.

It contains:

- Purchase details
- Gift card transaction information
- PayPal branding
- A **Cancel the Order** button

No attachments are included, making the embedded button the primary attack vector.

---

## Button Investigation

Inspecting the raw email source reveals that the **Cancel the Order** button redirects to a shortened URL instead of directly pointing to its final destination.

Using a URL shortening service allows attackers to hide the malicious website from the victim.

Instead of clicking shortened links directly, security analysts should investigate them safely using services such as:

- WhereGoes
- URLScan
- VirusTotal

These tools reveal the final destination without exposing the analyst to the malicious website.
