# Domain Controller and Print Server Configuration

## 1. Overview
This document outlines the step-by-step process of configuring a Windows Server as:
- **Domain Controller (DC)** for domain authentication and authorization.
- **Print Server** for centralized printer management.

---

## 2. System Information

| Component   | Details               |
|------------|-----------------------|
| **Server OS** | Windows Server (Version used) |
| **Domain Name** | `doc1.local` |
| **Server IP Address** | `172.20.75.3` |
| **Subnet Mask** | `255.255.248.0` |
| **Gateway** | `172.20.23.254` |
| **DNS Server** | `172.20.75.3 (Self)` |
| **Print Server Role** | Installed |

---

## 3. Domain Controller Configuration

### Step 1: Set Static IP Address
1. Open **Network and Sharing Center** → Click **Change adapter settings**.
2. Right-click the network adapter → Click **Properties**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → Click **Properties**.
4. Configure:
   - **IP Address**: `172.20.75.3`
   - **Subnet Mask**: `255.255.248.0`
   - **Default Gateway**: `172.20.23.254`
   - **Preferred DNS Server**: `172.20.75.3`
5. Click **OK** → Close all windows.

### Step 2: Install Active Directory Domain Services (AD DS)
1. Open **Server Manager** → Click **Manage** → **Add Roles and Features**.
2. Select **Role-based or feature-based installation** → Click **Next**.
3. Select **Active Directory Domain Services** → Click **Next**.
4. Click **Add Features** when prompted → **Next** → **Install**.
5. Once installed, click **Close**.

### Step 3: Promote Server to a Domain Controller
1. Open **Server Manager** → Click **Notification Flag** → **Promote this server to a domain controller**.
2. Select **Add a new forest**.
3. Enter **Root domain name**: `doc1.local` → Click **Next**.
4. Set **Directory Services Restore Mode (DSRM) Password** → Click **Next**.
5. Keep **default settings** → Click **Next** until **Install**.
6. The server will restart.

---

## 4. Creating Users and Organizational Units (OU)
### Step 1: Create Organizational Units (OUs)
1. Open **Active Directory Users and Computers** (`dsa.msc`).
2. Right-click the domain (`doc1.local`) → **New** → **Organizational Unit**.
3. Name it (e.g., "Users").
4. Repeat for other OUs (e.g., "Computers", "Groups").

### Step 2: Create a New User
1. Navigate to **Users OU**.
2. Right-click **Users** → **New** → **User**.
3. Enter:
   - **First Name**: John
   - **Last Name**: Doe
   - **User logon name**: `jdoe`
4. Click **Next** → Set a strong password.
5. Click **Finish**.

---

## 5. Print Server Configuration
### Step 1: Install Print Server Role
1. Open **Server Manager** → Click **Manage** → **Add Roles and Features**.
2. Select **Print and Document Services** → Click **Next**.
3. Select **Print Server** → Click **Next** → **Install**.

### Step 2: Add and Share a Printer
1. Open **Print Management** (`printmanagement.msc`).
2. Expand **Print Servers** → Right-click **Printers** → **Add Printer**.
3. Choose **TCP/IP Printer** and enter the printer’s IP address.
4. Select the printer model or install drivers.
5. Click **Next** → **Finish**.
6. Right-click the installed printer → **Printer Properties** → **Sharing** tab.
7. Check **Share this printer**, set a **share name** (e.g., `OfficePrinter`).

---

## 6. Testing and Troubleshooting
### Step 1: Verify Domain Connectivity
Run the following on a client PC:
```sh
ping 172.20.75.3
nslookup doc1.local
