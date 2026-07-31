
# JWT Secrets Investigation
![](Screenshot%202026-08-01%20004000.png)
## Overview

The JWT Secrets Investigation focused on analyzing a JSON Web Token (JWT) used to authorize privileged actions inside a simulated web application.

The objective of this challenge was to understand the JWT structure, identify sensitive information contained within the token, recover the signing secret, and generate a new valid token with reduced privileges.

The investigation combined JWT analysis, password cracking, and web security concepts to demonstrate how weak signing secrets can compromise authentication mechanisms.

---

# Scenario

During a security assessment, a suspicious high-privilege JWT was discovered inside an application ticket.

The token granted administrator access and contained a hidden clue embedded inside its payload. The task was to analyze the token, recover the signing secret, downgrade the user privileges, and generate a newly signed low-privilege JWT.

---

# Investigation Process

## Stage 1 – JWT Identification

The investigation started by identifying the token format.

The intercepted string consisted of three Base64URL encoded sections separated by periods, confirming that it was a JSON Web Token (JWT).

Analysis of the header identified the signing algorithm as **HS256**.

### Evidence

* Token Type: JWT
* Algorithm: HS256
![](844.png)
---

## Stage 2 – Token Structure Analysis

The token was decoded using JWT analysis tools.

Inspection of the payload revealed several important claims including:

* Username
* Issue timestamp
* Administrator privileges
* Hidden challenge flag

The payload contained:

```json
{
  "flag": "BTL{_4_Eyes}",
  "iat": 90000000,
  "name": "GreatExp",
  "admin": true
}
```

The hidden clue extracted from the payload was:

```
4_Eyes
```

### Evidence

![](846.png)

---

## Stage 3 – Secret Recovery

The signing secret protecting the JWT was recovered using **Hashcat**.

A dictionary attack using **rockyou.txt** failed to recover the secret.

A subsequent brute-force mask attack successfully recovered the signing key.

### Hashcat Command

```bash
hashcat -m 16500 jwt.txt ?a?a?a?a
```

Recovered Secret

```
bT!0
```

### Evidence

![](847.png)

---

## Stage 4 – Low Privilege Token Generation

After recovering the secret, a new JWT was generated.

The administrator privilege was modified from:

```json
"admin": true
```

to

```json
"admin": false
```

The modified payload was then re-signed using the recovered secret.

Generated JWT:

```text
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmbGFnIjoiQlRMe180X0V5ZXN9IiwiaWF0Ijo5MDAwMDAwMCwibmFtZSI6IkdyZWF0RXhwIiwiYWRtaW4iOmZhbHNlfQ.nMXNFvttCvtDcpswOQA8u_LpURwv6ZrCJ-ftIXegtX4
```

### Evidence

JWT.io Verification

---

# Challenge Answers

| Question          | Answer                   |
| ----------------- | ------------------------ |
| Token Name        | JWT                      |
| Token Structure   | Header.Payload.Signature |
| Hidden Hint       | 4_Eyes                   |
| Signing Secret    | bT!0                     |
| Low Privilege JWT | Successfully Generated   |

---

# Security Impact

The investigation demonstrated how weak JWT signing secrets significantly reduce authentication security.

Once the secret was recovered, it became possible to forge arbitrary JWTs, escalate or downgrade privileges, and impersonate other users.

Applications relying on weak HS256 secrets are vulnerable to token forgery attacks.

---

# MITRE ATT&CK Mapping

| Tactic            | Technique                     |
| ----------------- | ----------------------------- |
| Credential Access | Brute Force (T1110)           |
| Defense Evasion   | Valid Accounts (T1078)        |
| Credential Access | Unsecured Credentials (T1552) |

---

# Key Findings

* Identified the intercepted token as a JWT.
* Decoded and analyzed the JWT structure.
* Extracted sensitive claims from the payload.
* Recovered the JWT signing secret using Hashcat.
* Demonstrated successful brute-force recovery of a weak signing key.
* Generated a valid low-privilege JWT.
* Verified the new token using the recovered secret.
* Demonstrated the risks associated with weak JWT signing secrets.

---

# Tools Used

* Hashcat
* JWT.io
* Python 3
* PyJWT
* VS Code

---

# Skills Demonstrated

* Web Security
* JWT Analysis
* Authentication Security
* Password Cracking
* Hashcat
* JSON Web Token Analysis
* Privilege Manipulation
* Python Scripting
* Incident Analysis
* Security Assessment

---
![](Screenshot%202026-08-01%20003351.png)
