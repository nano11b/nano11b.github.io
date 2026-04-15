---
title: Configure MS Primary Domain Controller (MS-PDC)
date: 2026-04-14 12:00:00
categories: [Technology]
tags: [guides,science,computing] # TAG names should always be lowercase
---

Configuring **Windows Server 2022** as a **Primary Domain Controller (PDC)** means installing **Active Directory Domain Services (AD DS)** and promoting the server to a domain controller. Here’s a clean, professional step-by-step guide.

---

## 🧱 1. Prerequisites

Before you start:

* Set a **static IP address**
* Set the server’s **computer name** (e.g., `DC01`)
* Ensure proper **time sync**
* Use a strong **Administrator password**

---

## ⚙️ 2. Install Active Directory Domain Services

1. Open **Server Manager**
2. Click **Manage → Add Roles and Features**
3. Select:

   * **Role-based or feature-based installation**
4. Choose your server
5. Check:

   * ✅ **Active Directory Domain Services**
6. Click **Add Features**
7. Continue → **Install**

---

## 🚀 3. Promote Server to Domain Controller

After installation completes:

1. In **Server Manager**, click the notification flag
2. Click:
   👉 **Promote this server to a domain controller**

---

## 🌐 4. Deployment Configuration

Choose one:

### ➤ New Domain (most common)

* Select: **Add a new forest**
* Root domain name:

  ```
  yourdomain.local
  ```

  (Example: `corp.local`)

---

## 🔐 5. Domain Controller Options

* Set **Directory Services Restore Mode (DSRM) password**
* Keep defaults:

  * ✅ DNS Server
  * ✅ Global Catalog (GC)
* Leave site name as default unless needed

---

## 📁 6. Additional Options

* NetBIOS name auto-populates (e.g., `CORP`)
* Leave default paths unless you have a reason to change them:

  * NTDS
  * SYSVOL
  * Logs

---

## ✅ 7. Prerequisites Check & Install

* Click **Next → Install**
* Server will:

  * Configure AD
  * Reboot automatically

---

## 🧠 8. Post-Setup Verification

After reboot:

### Check AD is working:

* Open:

  * **Active Directory Users and Computers**
  * **DNS Manager**

### Verify:

* Domain is created
* DNS zone exists
* SYSVOL is shared:

  ```
  \\yourdomain.local\SYSVOL
  ```

---

## 🌍 9. Configure DNS (Important)

Set the server’s **preferred DNS** to itself:

```
127.0.0.1
```

or its static IP.

---

## 👥 10. Create Users & Join Clients

### Create a user:

* Open **Active Directory Users and Computers**
* Right-click domain → **New → User**

### Join a PC to the domain:

On a client machine:

1. Settings → System → About → **Rename this PC (Advanced)**
2. Click **Change**
3. Select:

   * **Domain**
4. Enter:

   ```
   yourdomain.local
   ```
5. Enter domain admin credentials
6. Reboot

---

## 🛡️ 11. Optional Hardening (Recommended)

* Enable **Windows Defender**
* Configure **Group Policy (GPO)**
* Disable unnecessary services
* Set up **backups** (critical for AD)

---

## ⚠️ Important Notes

* “Primary Domain Controller” is mostly a legacy term (from NT days).
  In modern AD, all domain controllers are **multi-master**, but your first one effectively acts as the primary.
* You can later add additional DCs for redundancy.
