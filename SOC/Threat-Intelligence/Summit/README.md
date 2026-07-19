# Summit
![Summit](Summit.png)
## Overview

**Summit** is one of the best practical Blue Team labs on TryHackMe. Instead of only learning theory, this room places you in the role of a Detection Engineer working alongside a Purple Team engagement.

Your mission is to continuously improve PicoSecure's security controls by detecting increasingly sophisticated malware samples. Each malware sample represents a higher level of the **Pyramid of Pain**, forcing defenders to rely on stronger detection mechanisms while making life progressively harder for attackers.

Throughout this lab, detection evolves from simple file hashes to attacker behaviors (TTPs), demonstrating why behavioral detection is the most powerful long-term defense.

---

# Learning Objectives

- Understand practical Detection Engineering
- Build detection rules for different Indicators of Compromise (IOCs)
- Learn how each Pyramid of Pain layer is implemented
- Create Firewall, DNS and Sigma rules
- Detect malware using behavioral analytics
- Understand how defenders increase attacker cost
- Gain hands-on Blue Team experience

---

# Scenario

PicoSecure hired an external penetration tester named **Sphinx** to simulate a real attacker.

Instead of stopping the attacker once, your job is to improve the organization's defenses after every malware execution.

Every time Sphinx bypasses your previous detection, you must build a stronger one.

Each malware sample represents another level of the **Pyramid of Pain**.

The journey looks like this:

```
Hash Detection
      ↓
IP Detection
      ↓
Domain Detection
      ↓
Host Artifacts
      ↓
Tool Detection
      ↓
Behavior (TTPs)
```

The higher you climb, the more expensive the attack becomes for the adversary.

---

# Sample 1 — Hash Detection
![Sample 1 - First Email](Sample1.exe%20and%20first%20email.png)
The first malware sample is extremely easy to detect.

After submitting the executable to the Malware Sandbox, the report reveals multiple Indicators of Compromise (IOCs), including the file's unique **MD5 hash**.
![Malware Sandbox](Malware%20Sandbox.png)
The solution is straightforward:

- Open **Manage Hashes**
- Add the malicious MD5 hash
- Save the detection rule

Because cryptographic hashes uniquely identify files, the malware is immediately blocked.

### Why it Works

Hashes provide extremely accurate detection.

If the file is identical, it will always produce the same hash.

![Sample1 Results](Sample1.exe%20results.png)
### Weakness

Changing even **one bit** inside the executable completely changes the hash.

Attackers simply recompile malware to evade this detection.

Because of this weakness, hashes sit at the **bottom of the Pyramid of Pain**.

### Detection Used

- MD5 Hash
- IOC Detection
- Static Detection
![Manage Hashes](Manage%20hashes%20window.png)
# Sample 2 — IP Address Detection

Sphinx recompiles the malware, generating a completely different hash.

The previous rule is now useless.

This time, the Malware Sandbox shows suspicious outbound network activity.
![Sample2 Results](Sample2.exe%20results.png)

Instead of detecting the file itself, we detect where the malware communicates.

Using the **Firewall Rule Manager**, create:

| Field | Value |
|--------|-------|
| Source | Any |
| Destination | 154.35.10.113 |
| Direction | Egress |
| Action | Deny |

Blocking outbound traffic prevents the malware from reaching its Command & Control (C2) server.
![Firewall Rule Manager](Firewall%20Rule%20Manager.png)
### Why Egress?

Ingress = Traffic entering the network.

Egress = Traffic leaving the network.

Since malware contacts the attacker's server, we block **outgoing traffic**.

### Advantages

- Blocks multiple malware samples using the same server.
- Stops Command & Control communication.

### Weakness

Attackers can simply move to another public IP address or cloud provider.

Therefore, IP addresses are also considered weak indicators.

### Detection Used

- Firewall Rule
- Network IOC
- C2 Detection


## What We Learned

After only two samples, we can already see why simple Indicators of Compromise eventually fail.

| Detection | Strength | Weakness |
|-----------|----------|----------|
| Hash | Very accurate | Changes after recompiling |
| IP Address | Blocks C2 | Easily changed by attackers |

As defenders, we must continue moving **up the Pyramid of Pain**, forcing attackers to spend more time, money, and effort to bypass our defenses.
# Sample 3 — Domain Detection

![Sample3 Results](Sample3.exe%20results.png)

After the firewall rule blocked the previous Command & Control (C2) IP address, the attacker changed the server's IP address and continued the attack.

The Malware Sandbox analysis revealed that the malware communicates with a suspicious domain instead of relying on a fixed IP address.

## Creating the DNS Rule

![DNS Rule Manager](DNS%20Rule%20Manager.png)

Open the **DNS Rule Manager** and create a new DNS rule using the following settings:

| Setting | Value |
|---------|-------|
| Rule Name | Any Name |
| Category | Malware |
| Domain | emudyn.bresonicz.info |
| Action | Deny |

This rule blocks DNS resolution for the malicious domain, preventing infected systems from reaching the attacker's infrastructure.

---

## Active DNS Rules

![Active Rules](Active%20rules%20overview.png)

After creating the rule, it appears in the list of active DNS rules.

From this point forward, any attempt to resolve the malicious domain will be denied before a network connection is established.

---

## Detection Method

- **IOC Type:** Domain Name
- **Pyramid of Pain Level:** Domain Names
- **Detection Confidence:** High
- **Attacker Cost:** Medium

Blocking domains is more effective than blocking IP addresses because attackers must register new domains, update DNS records, and modify their infrastructure before continuing the attack.

---

## Key Takeaways

- DNS filtering prevents malware from communicating with its Command & Control server.
- Domain-based detection is more resilient than IP-based detection.
- Security solutions frequently use DNS filtering to stop malware, phishing campaigns, and malicious websites before communication occurs.
