# Enterprise Browser Security Hardening & Download Restriction Using Active Directory GPO

This project simulates a real-world enterprise browser security control used to reduce malware infections, phishing attacks, ransomware delivery, drive-by downloads, and data exfiltration risks.

---

## Overview

This project demonstrates the implementation of an enterprise browser security baseline using Active Directory Group Policy Objects (GPO) and Google Chrome Enterprise Administrative Templates.

The goal was to reduce browser-based attack vectors commonly used in phishing campaigns, malware delivery, ransomware infections, drive-by downloads, and unauthorized data transfers.

The solution combines multiple security controls including:

* Download Restrictions
* Domain Allowlisting
* URL Blocklisting
* Browser Extension Control
* Safe Browsing Enforcement
* Incognito Mode Restriction
* Developer Tools Restriction
* Browser Hardening Policies

All controls are centrally managed through Active Directory and automatically enforced across domain-joined Windows endpoints.

---

## Lab Environment

* **Domain:** saada.local
* **Domain Controller:** Windows Server (Active Directory)
* **Client Machine:** Windows 10 (Domain Joined)
* **Browser:** Google Chrome Enterprise

---

## Technologies Used

* Active Directory Domain Services (AD DS)
* Group Policy Management Console (GPMC)
* Google Chrome Enterprise Administrative Templates (ADMX)
* Windows Server
* Windows 10 Enterprise

---


```
Enterprise Download Restriction GPO – Browser-Based Attack Mitigation/
|
├── README.md
|
├── architecture/
|   └── lab-diagram.png
|
├── before-policy/
|   ├── attachment-downloads/
|   |   ├── 01-Login Client Machine-.png
|   |   ├── 02-Sign In Gmail Account.png
|   |   ├── 03-Email Attachment Download.png
|   |   └── 04-Email Attachment Opened.png
|   ├── developer-tools-enabled/
|   |   └── 08-Developer tools are accessible.png
|   ├── downloads-allowed/
|   |   └── 10-Files can be downloaded from any source.png
|   ├── extensions-allowed/
|   |   └── 09-Browser extensions can be installed freely.png
|   ├── incognito-enabled/
|   |   └── 07-Incognito Mode is Available.png
|   └── unrestricted-web-access/
|       ├── 05-Access-To-Any Website.png
|       └── 06-Access-To-Any Website.png
|
├── after-policy/
|   ├── chrome-policy/
|   |   └── Chrome-Policies.png
|   ├── developer-tools-disabled/
|   |   └── Devtools-Disabled.png
|   ├── download-restriction/
|   |   ├── Email Attachment Download Blocked.png
|   |   ├── Gmail Sign In.png
|   |   └── Website Download Blocked.png
|   ├── extension-control/
|   |   └── Extension Installation Blocked.png
|   ├── gpresult/
|   |   └── gpresult policy applied.html
|   ├── incognito-disabled/
|   |   └── Incognito Mode Disabled.png
|   └── url-filtering/
|       ├── Authorized Domain allowed.png
|       └── Unauthorized Website Access Blocked.png
|
└── gpo-configuration/
    ├── chrome-deployment/
    |   ├── 02-Chrome installed.png
    |   ├── Assigned Package.png
    |   ├── Chrome Installed.png
    |   ├── GPO Linked to Domain.png
    |   ├── Shared Chrome Repository.png
    |   └── Software Installation Package.png
    ├── Developer tools policy/
    |   ├── Developer-Tools-Configuration-gpo.png
    |   └── Disallowing-Developer-Tools-gpo.png
    ├── Downloads policy/
    |   ├── 01-Block-All-Download-gpo.png
    |   └── 02-Block-All-Download-gpo.png
    ├── Extension policy/
    |   ├── 01-Configure-Extension-Block-List-gpo.png
    |   └── 02-Configure-Extension-Blocklist-gpo.png
    ├── gpo-creation/
    |   ├── 01-finding-group-policy-management.png
    |   ├── 01-gpmc-open.png
    |   ├── 02-create-gpo.png
    |   ├── 03-create-gpo.png
    |   ├── chrome-policy.png
    |   └── edit-gpo.png
    ├── Incognito policy/
    |   ├── 01-Incognito mode availability-gpo.png
    |   └── Incognito-mode-disabled-gpo.png
    ├── Safe browsing policy/
    |   ├── 02-Safe-Browsing-Protection-level-gpo.png
    |   └── Safe-Browsing-Protection-level-gpo.png
    ├── srp-gpo/
    |   ├── 02-srp-gpo-creation.png
    |   ├── downloads-path-rule.png
    |   ├── edge-blocked-message.png
    |   ├── edge-path-rule.png
    |   ├── security-filtering.png
    |   └── srp-gpo-creation.png
    ├── Urls filtering policy/
    |   ├── 01-Allow-Access-To-Urls-gpo.png
    |   ├── 01-Block-Access-To-Urls-gpo.png
    |   ├── 02-Allow-Access-To-Urls-gpo.png
    |   ├── 02-Block-Access-To-Urls-gpo.png
    |   └── 03-Allow-Access-To-Certain-Urls-gpo.png
    └── gpupdate.png
```


# Security Controls Implemented

| Control                     | Purpose                                       |
| --------------------------- | --------------------------------------------- |
| Download Restriction        | Prevent malicious file downloads              |
| URL Allowlist               | Allow only approved business websites         |
| URL Blocklist               | Block unauthorized websites                   |
| Extension Control           | Prevent installation of unapproved extensions |
| Safe Browsing Enforcement   | Protect users from phishing and malware       |
| Incognito Restriction       | Improve monitoring and policy enforcement     |
| Developer Tools Restriction | Reduce browser abuse opportunities            |
| Browser Hardening Baseline  | Standardize secure browser settings           |

---

## Architecture Diagram

This lab simulates a domain-controlled environment where browser security policies are centrally managed through Group Policy.

![Lab Diagram](architecture/lab-diagram.png)

### Policy Flow

1. User logs into a domain-joined Windows 10 workstation
2. Active Directory applies Group Policy
3. Google Chrome receives enterprise policy settings
4. Security controls are enforced automatically
5. User activity is restricted according to organizational policy

---

## Scenario

### Before Policy Implementation

* Users can access any website
* Attachments can be downloaded without restriction
* Browser extensions can be installed freely
* Incognito mode is available
* Developer tools are accessible
* Files can be downloaded from any source

📸 See screenshots in: `/before-policy/`

### After Policy Implementation

* Download attempts are blocked
* Unauthorized websites are restricted
* Browser extensions are controlled
* Safe Browsing is enforced
* Incognito mode is disabled
* Developer tools are disabled

📸 See screenshots in: `/after-policy/`

---

# Chrome Enterprise Policy Configuration

## Download Restrictions

Policy:

```text
DownloadRestrictions = Block all downloads
```

Purpose:

* Blocks all downloads
* Reduces malware delivery risk
* Mitigates ransomware infection vectors

---

## Domain Allowlisting

Policies:

```text
URLAllowlist
URLBlocklist
```

Example Configuration:

Allowed:

```text
https://github.com/*
https://*.microsoft.com/*
https://*.office.com/*
```

Blocked:

```text
*
```

Purpose:

* Restricts browsing to approved business websites
* Reduces exposure to phishing domains
* Limits access to malicious content

---

## Browser Extension Control

Policy:

```text
ExtensionInstallBlocklist = *
```

Purpose:

* all extensions are blocked by default. Extensions that are explicitly listed in the allowlist are allowed if they are signed.
* Reduces browser attack surface
* Mitigates credential theft and browser hijacking risks

---

## Safe Browsing Enforcement

Policy:

```text
SafeBrowsingProtectionLevel = 2
```

Purpose:

* Protects against phishing websites
* Detects malicious downloads
* Improves web threat protection

---

## Incognito Restriction

Policy:

```text
IncognitoModeAvailability = incognito mode disabled
```

Purpose:

* Improves visibility and accountability
* Prevents policy bypass attempts
* Ensures browser controls remain enforced

---

## Developer Tools Restriction

Policy:

```text
DeveloperToolsAvailability = disallow usage of the developer tools
```

Purpose:

* Reduces browser misuse
* Prevents unauthorized browser manipulation
* Supports endpoint hardening objectives

---

## Browser Hardening Baseline

Additional security controls enforced through Group Policy:

* Disable Password Manager
* Disable Credential Storage
* Disable Guest Mode
* Restrict Browser Extensions
* Force Safe Browsing
* Restrict Downloads
* Disable Incognito Mode
* Disable Developer Tools

These settings establish a secure browser baseline across all managed endpoints.

---

## Implementation Steps

### 1. Install Chrome ADMX Templates

Download the Google Chrome Enterprise Bundle.

Extract:

```text
Configuration\admx
```

Copy:

```text
chrome.admx
google.admx
```

To:

```text
C:\Windows\PolicyDefinitions
```

Copy language files:

```text
chrome.adml
google.adml
```

To:

```text
C:\Windows\PolicyDefinitions\en-US
```

---

### 2. Create Group Policy Object

Open:

```text
Group Policy Management Console (GPMC)
```

Create:

```text
Enterprise Browser Security Baseline
```

---

### 3. Configure Chrome Policies

Navigate to:

```text
User Configuration
 └ Policies
    └ Administrative Templates
       └ Google
          └ Google Chrome
```

Configure:

* Download Restrictions
* URL Allowlist
* URL Blocklist
* Extension Control
* Safe Browsing
* Incognito Restriction
* Developer Tools Restriction

---

### 4. Link and Deploy

Link the GPO to the domain or Organizational Unit (OU).

Apply:

```cmd
gpupdate /force
```

---

## Enforcing Chrome as the Sole Authorized Browser

### The Problem

Without additional controls, users can bypass all Chrome security policies by simply launching Microsoft Edge or Internet Explorer. These browsers:

- Are pre-installed on all Windows 10/11 devices
- May not have the same download restrictions, URL filtering, or Safe Browsing enforcement
- Represent a critical security gap in the enterprise browser security baseline

### The Solution

Three Group Policy configurations work together to ensure Chrome is the only browser users can access:

| Control | Purpose |
|---------|---------|
| **Deploy Chrome via GPO** | Ensures Chrome is installed on all domain-joined computers |
| **Block Microsoft Edge** | Prevents users from launching Edge to bypass policies |
| **Disable Internet Explorer** | Removes legacy browser access entirely |

---

## Method 1: Deploy Chrome Using GPO Software Installation (MSI)

### Step 1: Download Chrome Enterprise MSI

Go to:


Chrome Enterprise Download

Download: Google Chrome Enterprise MSI

Example file: GoogleChromeStandaloneEnterprise64.msi

---

### Step 2: Create a Shared Folder

On Domain Controller

Create:

C:\Software\Chrome

Copy the MSI file into this folder:

C:\Software\Chrome\GoogleChromeStandaloneEnterprise64.msi


### Step 3: Share the Folder

1. Right-click the Chrome folder

2. Select Properties → Sharing → Advanced Sharing

3. Check "Share this folder"

4. Set Share Name: Chrome

5. Click Permissions and add:
   
   Group                        Permission
   Everyone	                    Read
   Domain Computers	            Read

7. Click OK twice

 UNC Path:
  \\DC01\Chrome

 Full path to the MSI:
   \\DC01\Chrome\GoogleChromeStandaloneEnterprise64.msi


### Step 4: Verify Access

From your Windows 10 client (CLIENT01):

1. Press Windows + R

2. Type: \\DC01\Chrome

3. Verify you can see: GoogleChromeStandaloneEnterprise64.msi


### Step 5: Create Deployment GPO

Open Group Policy Management Console and create a new GPO:
Deploy Google Chrome

### Step 6: Edit the GPO
Navigate to:
Computer Configuration
 └ Policies
    └ Software Settings
       └ Software Installation

Right-click Software Installation → New → Package

⚠️ Important: Use UNC Path, NOT Local Path
✅ Correct	 \\DC01\Chrome\GoogleChromeStandaloneEnterprise64.msi	                                                                          ❌ Wrong   C:\Software\Chrome\GoogleChromeStandaloneEnterprise64.msi
	          


### Step 7: Choose Deployment Method

Select:
 Assigned
Click OK

### Step 8: Link the GPO
Link the Deploy Google Chrome GPO to:
saada.local
or specifically to any OU


### Step 9: Update Policy and Restart
On the Domain Controller:
 gpupdate /force

On the Windows 10 client:
 gpupdate /force
 shutdown /r /t 0


### Step 10: Verify Installation
After reboot, verify Chrome is installed:

Method A - Command Line:
chrome.exe

Method B - Control Panel:
Control Panel → Programs and Features
Chrome should appear in the installed programs list.

Method C - Chrome Policy Verification:

Open Chrome and go to:
chrome://policy
security policies should be active.


### Method 2: Software Restriction Policies (SRP)

### GPO Creation and Linking

Create a dedicated GPO specifically for blocking unauthorized browsers:

| Setting | Value |
|---------|-------|
| **GPO Name** | `Block Non-Chrome Browsers - SRP` |
| **Link Location** | `saada.local` (Domain root) |
| **Enforcement** | Enforced (Enabled) |

**Why link at the domain level?** Linking at the domain root ensures the policy applies to ALL computers and users, including future workstations that join the domain. This is standard enterprise practice for security baselines.
This GPO setting blocks specific executables from running, effectively removing alternative browsers as an option for end users 

#### Step 1: Create and Link the GPO

1. Open **Group Policy Management Console (GPMC)**
2. Right-click on `saada.local` → **Create a GPO in this domain, and Link it here...**
3. Enter the name: `Block Non-Chrome Browsers - SRP`
4. Click **OK**

The GPO is now created and automatically linked to the domain root.

#### Step 2: Edit the GPO

1. Right-click on the new GPO → **Edit**
2. Navigate to:

> `Computer Configuration` → `Policies` → `Windows Settings` → `Security Settings` → `Software Restriction Policies`

*If the folder is empty, right-click on **"Software Restriction Policies"** and select **"New Software Restriction Policies"** .*

#### Step 3: Create Path Rules

Right-click **"Additional Rules"** → **"New Path Rule..."** and configure the following:

| Application to Block | Path to Block | Security Level |
| :--- | :--- | :--- |
| **Microsoft Edge** | `%ProgramFiles(x86)%\Microsoft\Edge\Application\msedge.exe` | Disallowed |
| **Internet Explorer** | `%ProgramFiles%\Internet Explorer\iexplore.exe` | Disallowed |
| **Portable Executables** | `%UserProfile%\Downloads\*.exe` | Disallowed |

**Adding each rule:**
1. Select **"New Path Rule"**
2. Paste the path into the **Path** field
3. Set **Security level** to **Disallowed**
4. Click **OK**
5. Repeat for all three paths

> **Why block the Downloads folder?** Standard users cannot install software, but they might run "Portable" versions of browsers directly from their Downloads folder. This rule prevents any executable from running from that location, closing a major security gap.

#### Step 4: Configure Security Filtering (Optional but Recommended)

By default, the GPO applies to `Authenticated Users`. To ensure it applies correctly:

1. Select the GPO `Block Non-Chrome Browsers - SRP`
2. Click the **Scope** tab
3. Under **Security Filtering**, ensure `Authenticated Users` is present
4. (Optional) Add specific security groups if you need to exclude admins


#### Step 5: Verification

> **Important:** Computer Configuration policies (including AppLocker and Software Restriction Policies) require a reboot to fully apply. A simple `gpupdate /force` updates the registry, but the Application Identity Service and security policies do not fully activate until the next system startup.

### Order of Operations (Critical)

Policies must be applied in this specific order:

| Step | Machine | Command/Action | Why |
|------|---------|----------------|-----|
| 1 | **Domain Controller** | `gpupdate /force` | Ensures GPO changes are replicated to SYSVOL |
| 2 | **Domain Controller** | `shutdown /r /t 0` | DC reboot ensures security policies are loaded |
| 3 | **Wait 5 minutes** | - | Allows replication to complete |
| 4 | **Windows 10 Client** | `gpupdate /force` | Pulls latest GPO from DC |
| 5 | **Windows 10 Client** | `shutdown /r /t 0` | **REQUIRED** for AppLocker/SRP enforcement |
| 6 | **Windows 10 Client** | Log in after reboot | Policies now fully active |

### Step-by-Step Commands

**On the Domain Controller:**

gpupdate /force
shutdown /r /t 0


### Summary: Browser Enforcement GPOs

| GPO Name | Link Location | Purpose |
|----------|---------------|---------|
| `Enterprise Browser Security Baseline` | `saada.local` | Chrome security policies (downloads, URLs, extensions) |
| `Deploy Google Chrome` | `saada.local` | Installs Chrome MSI on all computers |
| `Block Non-Chrome Browsers - SRP` | `saada.local` | Blocks Edge, IE, and portable executables |

All three GPOs work together to ensure Chrome is the only available and properly secured browser in the domain.




# Security Validation Testing

## Test 1 – Email Attachment Download

Expected:

* Download blocked

Result:

* Successful enforcement

Screenshot:

```text
after-policy/download-restriction/email-download-blocked.png
```

---

## Test 2 – Website Download

Expected:

* Download blocked

Result:

* Successful enforcement

Screenshot:

```text
after-policy/download-restriction/website-download-blocked.png
```

---

## Test 3 – Unauthorized Website Access

Expected:

* Website blocked

Result:

* Successful enforcement

Screenshot:

```text
after-policy/url-filtering/site-blocked.png
```

---

## Test 4 – Extension Installation

Expected:

* Installation blocked

Result:

* Successful enforcement

Screenshot:

```text
after-policy/extension-control/extension-blocked.png
```

---

## Test 5 – Incognito Mode

Expected:

* Disabled

Result:

* Successful enforcement

Screenshot:

```text
after-policy/incognito-disabled/incognito-disabled.png
```

---

## Test 6 – Developer Tools

Expected:

* Disabled

Result:

* Successful enforcement

Screenshot:

```text
after-policy/developer-tools-disabled/devtools-disabled.png
```

---

## Test 7 – Policy Verification

Verification Method:

```text
On Windows 10 client, open Chrome and go to
chrome://policy
```

Policies Verified:

* DownloadRestrictions
* URLAllowlist
* URLBlocklist
* ExtensionInstallBlocklist
* SafeBrowsingProtectionLevel
* IncognitoModeAvailability
* DeveloperToolsAvailability

Screenshot:

```text
after-policy/chrome-policy/chrome-policy.png
```

---

## Test 8 – Group Policy Verification

Verification Method:

```cmd
gpresult /h report.html
```

Screenshot:

```text
after-policy/gpresult/gpresult-policy-applied.png
```

---

## Screenshots

### Before Policy

* User Login
* Email Access
* Successful Attachment Download
* Access any website
* Browser extensions can be installed freely
* Developer tools are accessible
* Incognito mode is available
* Files can be downloaded from any source

### GPO Configuration

* Group policy creation, linking to the domain(saada.local) and editing.
* Downloads policy
* Urls filtering policy
* Extension policy
* Incognito policy
* Developer tools policy
* Safe browsing policy
* Chrome Administrative Templates

### After Policy

* Download Blocked
* Website Blocked
* Extension Blocked
* Incognito Disabled
* Developer Tools Disabled

---

## Security Impact

* Prevents malware downloads
* Reduces phishing attack risk
* Mitigates ransomware delivery vectors
* Restricts unauthorized web access
* Supports Data Loss Prevention (DLP)
* Standardizes browser security controls
* Demonstrates centralized IT governance

---

## Protection Against Drive-By Downloads

By restricting browser downloads and enforcing Safe Browsing, this implementation significantly reduces exposure to drive-by download attacks.

This prevents users from unknowingly downloading malicious payloads from compromised websites.

---

# Security Outcomes

This implementation successfully:

* Reduced browser-based malware delivery risks
* Mitigated drive-by download attacks
* Restricted unauthorized website access
* Reduced browser extension attack surface
* Improved endpoint security standardization
* Supported DLP objectives through download control
* Strengthened phishing protection using Safe Browsing
* Centralized browser security management across the domain

---

## Compliance & Data Loss Prevention (DLP) Impact

This project enforces Data Loss Prevention (DLP) principles by restricting browser-based data exfiltration at the endpoint level. By controlling downloads, extensions, and unsafe browsing behavior through Active Directory GPO, sensitive data is prevented from leaving the organization through common attack vectors such as email attachments and web downloads.

Key DLP Controls Implemented
Control	Security Outcome
Download Restrictions	Prevents local storage of potentially sensitive files
URL Allowlist/Blocklist	Limits access to untrusted or malicious websites
Safe Browsing Enforcement	Reduces phishing and malware exposure
Extension Control	Prevents data leakage through malicious browser extensions
Compliance Framework Mapping
Framework	Alignment
ISO 27001	Endpoint security, malware protection, secure information transfer
NIST 800-53	Access control, data leakage prevention, secure configuration baselines
GDPR	Data protection by design, confidentiality, and secure processing
HIPAA	Safeguards for electronic protected health information (ePHI)
PCI DSS	Secure system configuration and access control enforcement

---

## Security Principles Demonstrated

* Least Privilege
* Defense in Depth
* Centralized Policy Enforcement
* Endpoint Hardening
* Browser Security Governance

---

## Key Learning Outcomes

* Active Directory Administration
* Group Policy Management
* Chrome Enterprise Administration
* Browser Security Hardening
* Endpoint Security Controls
* Data Loss Prevention Concepts
* Security Baseline Development
* Enterprise Security Operations

---

## Future Improvements

* USB Storage Restriction via GPO
* Application Whitelisting (AppLocker)
* Microsoft Defender Advanced Policies
* SIEM Integration (Splunk / Microsoft Sentinel)
* Security Event Monitoring
* Browser Security Reporting

---

## Author

**Abdirahman Ali**

GitHub: https://github.com/abdira

LinkedIn: https://www.linkedin.com/in/abdirahman-ali-5b8a2b3b4/

---

## Project Value

This project demonstrates practical enterprise-level experience with:

* Active Directory
* Group Policy
* Browser Security Hardening
* Endpoint Protection
* Data Loss Prevention
* Security Compliance Controls
* Enterprise Security Operations

making it highly relevant for System Administration, Blue Team, SOC Analyst, and Cybersecurity Engineering roles."
