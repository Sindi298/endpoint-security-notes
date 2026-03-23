## How to Identify Unsigned Binaries

### What is a digital signature?
A digital signature cryptographically proves that a file was created by a 
specific organisation and has not been modified since signing. Legitimate 
software from major vendors is always signed.

### How to check in VirusTotal
1. Submit the file hash to VirusTotal
2. Go to the **Details** tab
3. Scroll to **Signature Info**
4. Look for **"Signature verification"** at the top

### What you'll see
| Result | Meaning |
|--------|---------|
| Valid signature — Vendor Name | File is legitimately signed — lower suspicion |
| File is not signed | No valid signature — escalate investigation |
| Signed but certificate metadata present | Possible trojanized installer — file modified post-signing |

### Real world example
During an Opera installer investigation, the file contained x509 certificate 
metadata referencing Opera Norway AS and DigiCert — but signature verification 
returned "File is not signed." This indicated the file had been modified after 
the original signing, invalidating the cryptographic signature. A 2.56MB 
overlay with 7.999 entropy corroborated this conclusion.

### Why it matters
- Legitimate installers from major vendors are always signed
- Metadata can be spoofed — anyone can write "Opera Software" in a file
- Only the cryptographic signature proves authenticity
- An unsigned binary claiming to be from a known vendor is a critical red flag

## Entropy Analysis

### What is entropy?
Entropy measures the randomness of data in a file. It is scored on a scale 
of 0 to 8, where 0 is completely predictable and 8 is completely random.

### Why it matters in malware analysis
Legitimate software has predictable entropy patterns across its sections. 
Malware authors use encryption and packing to hide malicious payloads — 
both of which produce high entropy values.

### Entropy reference table
| Entropy Range | Meaning |
|--------------|---------|
| 0.0 — 3.0 | Very low — plain text, simple data |
| 3.0 — 6.5 | Normal — typical compiled code |
| 6.5 — 7.5 | Elevated — compressed data, some packers |
| 7.5 — 8.0 | Critical — strongly indicates encryption or packing |

### How to check in VirusTotal
1. Submit the file hash to VirusTotal
2. Go to the **Details** tab
3. Scroll to **PE Info** section
4. Look at entropy values for each section
5. Pay special attention to any **Overlay** section

### Section vs Overlay
| Location | Significance |
|----------|-------------|
| High entropy in .text section | May indicate packed executable |
| High entropy in overlay | Strongly indicates appended payload |

### Real world example
During an Opera installer investigation, File 2 contained an overlay section 
of 2.56MB — nearly the entire file size of 2.78MB — with an entropy value 
of 7.999, approaching the theoretical maximum of 8.0. All other sections 
showed normal entropy between 4.08 and 6.61. This single finding was the 
strongest indicator of malicious intent in the entire investigation.

### Key takeaway
Never ignore a high entropy overlay. A legitimate installer does not need 
to append 2.56MB of near-maximum entropy data to itself.

## Ad Network Distribution & UTM Parameters as IOCs

### How malware gets delivered via popup ads
Malicious actors purchase advertising space on legitimate ad networks to 
distribute malware. When a user visits a website, a popup ad triggers an 
automatic or user-initiated file download. The file is named to appear 
legitimate — in this case, OperaSetup.exe.

### Why ad network distribution is always suspicious
- Official software is distributed via the vendor's official domain
- No legitimate vendor distributes installers via popup ads
- Ad networks like Admaven are known for distributing bundleware and PUPs
- Files from ad networks should always be treated as untrusted regardless 
  of file name or metadata

### UTM Parameters as IOCs
UTM parameters are tracking tags appended to URLs by advertisers. They 
reveal the distribution source and campaign details of a file download.

### Common UTM parameters
| Parameter | Meaning |
|-----------|---------|
| utm_source | The ad network or platform that served the ad |
| utm_medium | The ad format — banner, popup, email etc |
| utm_campaign | The specific campaign name |
| utm_country | The targeted country |

### Real world example
During an Opera installer investigation, VirusTotal revealed the following 
UTM parameters embedded in the file:

| Parameter | Value | Significance |
|-----------|-------|-------------|
| utm_source | admaven | Confirms Admaven ad network as distribution source |
| utm_medium | apb | Ad format — automatic popup banner |
| utm_campaign | popup | Confirms popup ad delivery method |
| utm_country | ZA | Confirms South African users were targeted |

These parameters confirmed the files did not originate from opera.com and 
were part of a targeted ad campaign distributing trojanized installers.

### Where to find UTM parameters in VirusTotal
1. Submit the file hash to VirusTotal
2. Go to the **Details** tab
3. Scroll to **File Version Information** or **Contacted URLs**
4. Look for utm_ prefixed parameters in any URLs present

### Key takeaway
UTM parameters are not just marketing data — in a malware investigation 
they are IOCs that reveal distribution infrastructure, targeting, and 
campaign details. Always extract and document them.

