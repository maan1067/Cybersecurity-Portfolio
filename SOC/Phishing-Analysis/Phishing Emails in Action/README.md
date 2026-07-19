# Phishing Emails in Action

![Phishing Emails in Action](Phishing%20Emails%20in%20Action.png)

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

Check out **Phishing Analysis Fundamentals** for an overview of email communications and analysis.

---

# Cancel Your Order

In this task, we will examine a sample email designed to mimic an official transaction receipt from **PayPal**. By analyzing this specific sample, we will focus on how attackers leverage spoofed email addresses to impersonate trusted services and the strategic use of URL shortening services to obfuscate the final destination of malicious links.

---

## Phishing Techniques Used

The phishing email uses several social engineering techniques:

- **Spoofed Email Address** – Mimicking a trusted service to gain immediate credibility.
- **URL Shortening** – Using redirection services to hide the true destination of a malicious link.
- **Branded HTML** – Impersonating legitimate corporate imagery to create a sense of authenticity.

---

## First Observations

![First Observations](First%20Observations.png)

Let's first look at the sample email header and take a few notes on our immediate observations.

- **Attention-grabbing Subject Line:** Uses a fake transaction to create urgency and pressure the victim into reacting quickly.
- **From Address:** The sender appears as **service@paypal.com**, but the actual email originates from **gibberish@sultanbogor.com**, which is a major red flag.
- **To Address:** The recipient email is unusual and does not resemble a normal Yahoo email account.

These inconsistencies are enough to immediately classify the email as suspicious before inspecting its contents.

---

## Email Body Analysis

![Email Body Analysis](616945d482ef350052080da1-1774315608150.svg)

The email body is designed to closely resemble a legitimate PayPal purchase receipt.

It includes:

- Purchase details
- Gift card transaction information
- Official-looking PayPal branding
- A **Cancel the Order** button

There are **no attachments** in this sample. Instead, the attacker relies entirely on convincing the victim to click the embedded button.

---

## Button Investigation

![Button Investigation](Button%20Investigation.png)

By inspecting the raw email source, we can investigate the hyperlink hidden behind the **Cancel the Order** button.

Instead of linking directly to its final destination, the button points to a **shortened URL**. URL shortening services hide the real destination, making it difficult for users to determine whether a link is legitimate or malicious.

For this reason, security analysts should **never click shortened URLs directly** during an investigation.

---

## Investigating Shortened URLs

![WhereGoes](WhereGoes.png)

Thankfully, several online tools allow analysts to safely inspect shortened URLs without visiting the destination website.

One example is **WhereGoes**, which follows the redirect chain and reveals the final destination safely.

Using tools like this helps analysts determine whether a link points to:

- A legitimate website
- A phishing page
- A malware download
- A credential harvesting portal

without exposing themselves to unnecessary risk.

# Track Your Package

The second phishing sample imitates a shipping notification to create urgency and trick the recipient into clicking a malicious tracking link. Unlike the previous example, this campaign also uses **tracking pixels** to notify the attacker when the email has been opened.

## Phishing Techniques Used

- **Spoofed Email Address:** Pretending to be a trusted distribution center.
- **Pixel Tracking:** Embedding invisible images that notify the attacker when the email is opened.
- **Link Manipulation:** Hiding a malicious destination behind what appears to be a legitimate tracking number.

---

## First Observations

![First Observations](First%20Observations.png)

The email immediately raises several red flags:

- **Subject Line:** Uses a fake tracking number to create urgency and pressure the recipient into clicking.
- **From Address:** The display name is **Distribution Center**, but the real sender is **contact@beginpro.club**, which is suspicious.
- **Hyperlink:** The tracking number looks legitimate, but its destination is hidden.

### Red Flags

- Display name does not match the actual sender address.
- Sense of urgency to encourage immediate action.
- Suspicious tracking link that may redirect to a phishing website.

> **Note:** Yahoo automatically blocked the images and hyperlinks in this email. Many email providers do this because attackers frequently abuse externally loaded images for tracking purposes.

---

## Hyperlink Tracking

![Hyperlink Tracking](Hyperlink%20Tracking.svg)

Inspecting the raw source of the email reveals the use of a **tracking pixel**.

A tracking pixel is a tiny invisible image embedded inside an email. When the recipient opens the email and the image loads, it silently contacts the attacker's server and can reveal:

- That the email has been opened.
- The time it was opened.
- The recipient's IP address.
- Device or email client information.
- Sometimes the recipient's approximate geographic location.

This explains why many email providers block remote images by default.

### Why Attackers Use Tracking Pixels

- Confirm that an email address is active.
- Identify users who interact with phishing emails.
- Launch more targeted phishing attacks.
- Measure the success of phishing campaigns.

### Analyst Takeaway

When analyzing phishing emails:

- Never trust hyperlinks based only on their displayed text.
- Inspect the raw email source whenever possible.
- Be cautious with externally loaded images because they may be tracking pixels.
- Keep automatic image loading disabled while performing email analysis.
