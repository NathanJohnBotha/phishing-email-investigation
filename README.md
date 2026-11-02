## 1. Project Overview 

Conducted phishing email analysis using Vim (a text editor) in Kali Linux to inspect a raw .eml file, manually extract IOCs, and analyze suspicious indicators with CyberChef and VirusTotal, identifying a likely phishing URL. 

## 2.Tools used

   Kali linux
   Vim ( Text Editor) 
   VirusTotal
   Cyberchef

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

**Assessment:** The sender-domain inconsistency and Reply-To mismatch warrant further investigation. These observations alone are insufficient to confirm phishing.


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
* **Infrastructure:** Microsoft Exchange Online Protection
* **Timestamp:** 27 April 2026, 14:04:52 UTC
* **Transport Security:** TLS 1.3

### Assessment

The email headers indicate that the message was processed through Microsoft email infrastructure. The sending IP address was identified for further reputation analysis.


## 5. Email Authentication Analysis
   - Screenshot 3
   - Findings

## 6. Email Body Analysis
   - Screenshot 4
   - Findings

## 7. IP Reputation Analysis
   - Screenshot 5
   - Findings

## 8. Domain Reputation Analysis
   - Screenshot 6
   - Findings

## 9. URL Reputation Analysis
   - Screenshot 7
   - Findings

## 10. Final Verdict

## 11. Recommended Remediation
