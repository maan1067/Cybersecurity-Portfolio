# Squid Game – Steganography Investigation

## Overview

The **Squid Game** challenge from **Blue Team Labs Online (BTLO)** is a medium-difficulty steganography challenge worth **20 points**.

The objective is to investigate a Squid Game invitation card, identify information through online research, extract a hidden file from the invitation, analyze the extracted image for a hidden hint, and finally recover the challenge flag.

The challenge provides the following tools as suggested resources:

* **Google**
* **Steghide**
* **Stegsolve.jar**
* **Python**

---

# Scenario

The challenge presents a simple scenario:

> **Will you survive the Squid Games?**

The investigation follows a multi-stage hidden-data extraction process.

The challenge questions were:

1. What is the phone number on the invitation card in Squid Game?
2. Can something be extracted from the invitation card file, and what is the filename?
3. What hint text can be discovered in the final file?
4. What is the final flag?

---

# Challenge Information

| **Property**         | **Value**                           |
| -------------------- | ----------------------------------- |
| **Platform**         | Blue Team Labs Online               |
| **Challenge**        | Squid Game                          |
| **Difficulty**       | Medium                              |
| **Points**           | 20                                  |
| **Category**         | Steganography / Digital Forensics   |
| **Suggested Tools**  | Google, Steghide, Stegsolve, Python |
| **Archive Password** | `btlo`                              |

---

# Investigation Process

---

## Stage 1 – Invitation Card Research

The first question specifically instructs the analyst to research the invitation card online.

The phone number associated with the Squid Game invitation card was identified through online research.

### Finding

```text
86504006
```

### Challenge Answer

`86504006`

This information is important because the challenge's next stage involves extracting hidden content from the invitation card.

---

# Stage 2 – Steghide Extraction

The invitation card file was analyzed as a potential steganography container.

Since **Steghide** was listed as one of the recommended tools, it was used to check for embedded data inside the image.

The extraction command was:

```bash
steghide extract -sf "Invitation Card.jpg"
```

The extraction process revealed a hidden file.

### Extracted File

```text
Dalgona.png
```

### Challenge Answer

`Dalgona.png`

This established that the invitation card was being used as the first steganographic container.

---

# Stage 3 – Analysis of Dalgona.png

The extracted file was:

```text
Dalgona.png
```

The challenge specifically provides **Stegsolve.jar**, making image-plane analysis the next logical step.

The image was opened with Stegsolve and its different color planes were inspected.

During the color-plane analysis, hidden text was discovered.

### Hidden Hint

```text
red pixel
```

### Challenge Answer

`red pixel`

The hint indicates that the next stage should focus specifically on the **red color channel/pixel values**.

---

# Stage 4 – Red Pixel Analysis

Following the discovered hint:

```text
red pixel
```

the red-channel values of the relevant pixels were extracted from the image.

The resulting values were:

```text
123, 102, 124, 173, 123, 64, 166, 63, 137, 115, 171, 64,
156, 155, 64, 162, 137, 107, 165, 171, 65, 175
```

These values represented encoded character data.

The values were then interpreted and converted into ASCII characters.

---

# Stage 5 – ASCII Conversion

After converting the extracted values into their corresponding ASCII representation, the final flag was recovered.

### Decoded Flag

```text
SBT{S4v3_My4nm4r_Guy5}
```

### Challenge Answer

`SBT{S4v3_My4nm4r_Guy5}`

---

# Complete Attack / Investigation Chain

The entire challenge can be represented as:

```text
Invitation Card
        ↓
Online Research
        ↓
86504006
        ↓
Steganography Analysis
        ↓
Dalgona.png
        ↓
Stegsolve
        ↓
"red pixel"
        ↓
Red Channel / Pixel Values
        ↓
ASCII Conversion
        ↓
SBT{S4v3_My4nm4r_Guy5}
```

---

# Challenge Answers Summary

| **Question**            | **Answer**               |
| ----------------------- | ------------------------ |
| **Q1 – Phone Number**   | `86504006`               |
| **Q2 – Extracted File** | `Dalgona.png`            |
| **Q3 – Hint Text**      | `red pixel`              |
| **Q4 – Final Flag**     | `SBT{S4v3_My4nm4r_Guy5}` |

---

# Key Findings

* The Squid Game invitation card contained hidden steganographic data.
* Online research revealed the phone number `86504006`.
* The invitation card contained an embedded file named `Dalgona.png`.
* Stegsolve color-plane analysis revealed the hint `red pixel`.
* The red-channel pixel values contained the final encoded data.
* ASCII conversion produced the final flag.

---

# Tools Used

### Google

Used for researching the phone number associated with the Squid Game invitation card.

### Steghide

Used to extract hidden data embedded inside the invitation image.

```bash
steghide extract -sf "Invitation Card.jpg"
```

### Stegsolve

Used to inspect the extracted PNG through different image color planes and identify the hidden `red pixel` hint.

### Python / ASCII Analysis

Used as an appropriate method for processing the extracted numerical pixel values and converting the encoded data into readable characters.

---

# Shortest / Fastest Path

The shortest verified investigation path was:

```text
Google
→ 86504006
→ Steghide
→ Dalgona.png
→ Stegsolve
→ "red pixel"
→ Red-channel values
→ ASCII
→ SBT{S4v3_My4nm4r_Guy5}
```

No unnecessary forensic analysis was required once each stage provided a clear direction for the next stage.

---

# Final Result

**Challenge:** Squid Game
**Points:** 20/20

### Final Flag

```text
SBT{S4v3_My4nm4r_Guy5}
```

### Skills Demonstrated

* Digital Forensics
* Image Steganography
* Steghide Extraction
* Image Color-Plane Analysis
* Stegsolve
* Pixel Analysis
* ASCII Encoding/Decoding
* Evidence-Based CTF Solving
* Multi-Stage Data Extraction
