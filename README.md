# hosting_domain_M365_protecting_with_sophosEmail
Hosting my domain on M365 and protecting it via Sophos Email

TABLE OF CONTENT
1. [Introduction](#introduction)
2. [Project Overview](#project-overview)
3. [Requirements](#requirements)
4. [Setup Steps](#setup-steps)
    - [Domain Configuration](#1-domain-configuration)
    - [M365 Integration](#2-m365-integration)
    - [Sophos Email Protection Setup](#3-sophos-email-protection-setup)
5. [Testing](#testing)
6. [Troubleshooting](#troubleshooting)
7. [Future Enhancements](#future-enhancements)
8. [Acknowledgments](#acknowledgments)
   

## INTRODUCTION:

In this project, I document the steps and troubleshooting steps involved in hosting my domain on Microsoft 365 and protecting it via Sophos Email.


## PROJECT OVERVIEW

- **Domain**: [your-cybergirl.in);
- **Email Hosting**: Microsoft 365
- **Security Solution**: Sophos Email
- **Key Objectives**:
  - Enable global email communication for the domain.
  - Protect emails from phishing, malware, and spam.
  - Optimize email delivery with proper DNS configurations.

## EMAIL FLOW 

+----------------------+                     +----------------------+                     +-------------------+
|                      |                     |                      |                     |                   |
|      Internet        +-------------------->+    Sophos Email      +-------------------->+    Microsoft 365  |
|                      |                     |  (Inbound Scanning)  |                     |  (Inbound Email)  |
+----------------------+                     +----------------------+                     +-------------------+
                                                                                                 |
                                                                                                 |
                                                                                                 v
                                                                                   Emails delivered to M365 mailboxes
                                                                                 
Inbound Email Flow:
1. Email is sent from the internet to the domain's MX records, which point to Sophos Email.
2. Sophos Email scans inbound emails for spam, phishing, and malware.
3. After scanning, Sophos Email routes the email to Microsoft 365.
4. Microsoft 365 accepts the email using inbound connectors.

======================================================================================================

+----------------------+                     +----------------------+                     +-------------------+
|                      |                     |                      |                     |                   |
|    Microsoft 365     +-------------------->+    Sophos Email      +-------------------->+    Recipient       |
|  (Outbound Email)    |                     |  (Outbound Scanning) |                     |      Domain        |
+----------------------+                     +----------------------+                     +-------------------+
                                                                                                 |
                                                                                                 |
                                                                                                 v
                                                                                   Emails delivered to recipient

Outbound Email Flow:
1. Outbound email originates from Microsoft 365.
2. Microsoft 365 routes the outbound email to Sophos Email using an outbound connector.
3. Sophos Email scans the outbound email for threats.
4. Sophos Email delivers the scanned email to the recipient's domain.


## Requirements

- Purchased domain: `your-cybergirl.in`
- Active Microsoft 365 subscription.
- Sophos Email Protection subscription.
- Administrative access to:
  - Domain registrar (e.g., GoDaddy).
  - Sophos Central dashboard.
  - M365 Admin Center.

## Setup Steps

### 1. Domain Configuration
1. Purchase a domain from a registrar (e.g., GoDaddy).

### 2. M365 Integration
1. Add the domain in M365 Admin Center.
2. Verify ownership of the domain.
3. Assign email licenses to users.

### 3. Sophos Email Protection Setup
1. Verify domain ownership on Sophos Email
2. Setup Inbound communication configurations: https://techvids.sophos.com/watch/TJ4MLodKLYmq6ABSdyDq1B
3. Setup Outbound communication configurations: https://techvids.sophos.com/watch/NYLKjabWcJ4JUiNRwPQwSC
4. Add the user mailbox on Sophos Email

### 4. Troubleshooting steps

My outbound communication was working fine after following all the steps.
However, for the inbound communication, emails were being non-delivered. 

It was happening because of incorrect inbound destination configured on Sophos Email.
We need proper MX hosts of M365 to be configured on Sophos Email to be able to route the received inbound emails to M365. 
To generate MX hosts of M365, follow below steps:

1. Login to M365 admin center
2. Go to Settings > Domains
3. Select your domain > DNS records > Setup DNS records (As you have purchased the domain from Go Daddy, it will connect with Go Daddy)
4. M365 will automatically generate the DNS recors (MX) and will be publishing it on Go Daddy DNS recors.
5. It will override the previously hosted MX records of Sophos. We need to edit those MX records on Godaddy again and keep Sophos MX records with high priority than M365.
6. That automatically created MX host address of M365 needs to be configured on Sophos Email domain settings as Inbound gateway.
