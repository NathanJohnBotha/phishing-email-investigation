## 1. Project Overview 

Conducted phishing email analysis using Vim (a text editor) in Kali Linux to inspect a raw .eml file, manually extract IOCs, and analyze suspicious indicators with CyberChef and VirusTotal, identifying a likely phishing URL. 

## 2.Tools used

   Kali linux, Vim ( Text Editor), VirusTotal, Cyberchef

## 3. Email Overview - 

### Methodology

Opened the raw `.eml` file using Vim in Kali Linux to manually inspect the email metadata, including the sender, recipient, subject, date, Reply-To address, and Return-Path.

### Evidence

**Screenshot 1 — Email Overview**

<img width="2558" height="1431" alt="01-email-overview png" src="https://github.com/user-attachments/assets/df955f30-167e-471c-ba3b-7d6cb6b6c2a1" />


### Findings

| Field        | Value                                |
| ------------ | ------------------------------------ |
| Display Name | Your Respiratory Health Guide        |
| Sender       | `thanhntn94@stu.tdt.edu.vn`          |
| Recipient    | `phishing@pot`                       |
| Subject      | The Secret to Healthy Lungs Revealed |
| Date         | 27 April 2026, 14:03:52 UTC          |
| Reply-To     | `reply@2ndal7.com`                   |
| Return-Path  | `thanhntn94@stu.tdt.edu.vn`          |

**Initial Observations:**

* The sender used an academic student email domain (`stu.tdt.edu.vn`) while presenting the message as respiratory health information.
* The Reply-To domain (`2ndal7.com`) differed from the sender's domain, indicating that responses would be directed to a separate domain.
* The subject line used curiosity-driven health messaging to encourage engagement.

**Assessment:** The sender-domain inconsistency and Reply-To mismatch warrant further investigation. The display name, "Your Respiratory Health Guide," presents the email as a health-related service, while the sender's address belongs to an academic student domain.


## 4. Email Header Analysis

### Methodology

Manually examined the `Received` headers in Vim to identify the sending IP address, mail servers, and email routing information.

### Evidence

**Screenshot 2 — Email Header Analysis**

<img width="2558" height="1431" alt="01-email-overview png" src="https://github.com/user-attachments/assets/fdc37b7e-fcb7-47f7-8704-41c294ffd8f2" />


### Findings

* **Sending IP:** `40.107.75.99`
* **Sending Server:** `OS8PR02CU002.outbound.protection.outlook.com`
* **Receiving Server:** `BL6PEPF0001AB4F.mail.protection.outlook.com`
* **Receiving Server IP:** `10.167.242.73`
* **Timestamp:** 27 April 2026, 14:04:52 UTC


### Assessment

The email headers indicate that the message was processed through Microsoft email infrastructure. The sending IP address was identified for further reputation analysis.


## 5. Email Authentication Analysis

### Methodology

Manually examined the email authentication headers in Vim to assess SPF, DKIM, and DMARC results and identify potential sender authentication inconsistencies.

### Evidence

**Screenshot 3 — Email Authentication Analysis**

<img width="2558" height="1431" alt="01-email-overview png" src="https://github.com/user-attachments/assets/97d30f84-d41b-4bc8-8109-4f0839d5cecf" />


### Findings

**Authentication-Results:**

* SPF: `none`
* DKIM: `none`
* DMARC: `none`
* Composite Authentication: `pass`

**ARC-Authentication-Results:**

* SPF: `pass`
* DKIM: `pass`
* DMARC: `pass`

### Assessment

The email contains differing authentication results. The Authentication-Results header reports SPF, DKIM, and DMARC as `none`, while an ARC-Authentication-Results header records successful authentication checks.


## 6.Email Body Analysis

### Methodology

Identified Base64-encoded HTML content within the raw `.eml` file using Vim. Extracted the encoded content and decoded it using CyberChef to examine the email body and identify embedded URLs.

### Evidence

**Screenshot 4 — Decoded Email Body Using CyberChef**

<img width="2558" height="1431" alt="Screenshot_2026-11-02_08_31_12" src="https://github.com/user-attachments/assets/89cb7292-88f9-468f-b555-80b7618fd9e7" />

<img width="2558" height="1431" alt="Screenshot_2026-11-02_10_23_27" src="https://github.com/user-attachments/assets/491b1c7d-b2a2-4299-a680-f4f29eb61c25" />


### Findings

* **Content Type:** HTML
* **Encoding:** Base64
* **Decoding Tool:** CyberChef
* **Tracking Domain:** `track.kolabokoliya.vip`
* **Tracking Endpoint:** `/track_click.php`
* **Embedded Destination:** `storage.googleapis.com/seawcdef/pulmo-Balance.htm`

The decoded email contained health-related messaging referencing headaches, chest tightness, brain fog, and respiratory concerns.

Multiple hyperlinks directed recipients through a tracking endpoint containing an encoded URL pointing to an external HTML page hosted on Google Cloud Storage.

### Assessment

The email uses health-related messaging and repeated hyperlinks to encourage recipient engagement.


## 7.IP Reputation Analysis

### Methodology

Extracted the sending IP address (`40.107.75.99`) from the email headers and investigated its reputation using VirusTotal.

### Evidence

**Screenshot 5 — VirusTotal IP Reputation Analysis**

<img width="2558" height="1431" alt="Screenshot_2026-11-02_10_33_36" src="https://github.com/user-attachments/assets/dc8d8148-6fb3-4050-b0e3-5bd26809bb47" />


### Findings

* **IP Address:** `40.107.75.99`
* **Detection Ratio:** 0/92
* **Organization:** Microsoft Corporation
* **Country:** Japan (JP)

VirusTotal reported nothing malicious. 

The IP address is associated with Microsoft Corporation, consistent with the Microsoft email identified during the header analysis.

### Assessment

The sending IP address was not flagged as malicious by VirusTotal.

Although the IP address belongs to legitimate Microsoft infrastructure, this does not establish that the email itself is legitimate.

The email's suspicious content and embedded URLs require further investigation to determine whether the message represents a phishing attempt.


## 8. Domain Reputation Analysis

### Methodology

Extracted the domain `track.kolabokoliya.vip` from the decoded HTML email body and investigated its reputation using VirusTotal. Reviewed security vendor detections and classifications to identify potential associations with malicious or suspicious activity.

### Evidence

**Screenshot 6 — VirusTotal Domain Reputation Analysis**

<img width="2558" height="1431" alt="Screenshot_2026-11-02_10_37_32" src="https://github.com/user-attachments/assets/2a3f94e6-134f-4f82-849a-ee518d331296" />


### Findings

* **Domain:** `track.kolabokoliya.vip`
* **Malicious Detections:** 0/92
* **Suspicious Classifications:** 2
* **Gridinsoft:** Suspicious
* **LevelBlue:** Suspicious

VirusTotal reported no malicious detections from the 92 security vendors. However, Gridinsoft and LevelBlue classified the domain as suspicious.

The domain was identified within the decoded email body and appeared in hyperlinks using the `/track_click.php` endpoint.

### Assessment

The domain's suspicious

## ## 9. URL Reputation Analysis

### Methodology

Extracted the destination URL from the decoded HTML email body and investigated its reputation using VirusTotal.

### Evidence

**Screenshot 7 — VirusTotal URL Reputation Analysis**

<img width="2558" height="1431" alt="Screenshot_2026-11-02_10_41_18" src="https://github.com/user-attachments/assets/f5fd4be1-8a7f-4807-93eb-8122c99df586" />


### Findings

* **Destination URL:** `hxxps://storage[.]googleapis[.]com/seawcdef/pulmo-Balance.htm`
* **Detection Ratio:** 2/93
* **Phishing Database:** Phishing
* **SafeToOpen:** Phishing
* **HTTP Response:** 403


VirusTotal reported that two security vendors classified the destination URL as phishing.

The URL was identified within the decoded HTML email body and referenced through hyperlinks using the `track.kolabokoliya.vip` tracking domain.

### Assessment

The destination URL's phishing classifications provide evidence supporting the possibility of a phishing attempt.


Although only two security vendors classified the URL as phishing, the combined findings increase confidence that the email is likely

