

# 🏗️ On-Premises AD + Exchange → Microsoft 365 Hybrid Lab (Simulation)

## 📌 Overview
This lab simulates a hybrid migration project for a 20-user company moving from on-premises Active Directory + Exchange Server 2019 into Microsoft 365.  
It covers directory sync, hybrid identity, and Exchange hybrid connectors.  
> ⚠️ Internet-facing mail flow (public DNS, certs, static IP) was not configured — this is a **simulation lab**.

---

## 🔹 Phase 1 — On-Prem AD Foundation
- Built **DC01** (Domain Controller).
- Configured **static IP + DNS**.
- Created **`weepwaap.lab` domain**.
- Built OUs:
  - `Lab Users` (HR, Finance, IT)
  - `Lab Computers` (Workstations, Servers)
- Bulk-created **15 AD users**.

📸 *[Screenshot: ADUC with users + OUs]*

---

## 🔹 Phase 2 — Exchange On-Prem Setup
- Built **EX01**, installed **Exchange Server 2019**.
- Enabled mailboxes for all 15 AD users.
- Verified **OWA login** + on-prem mail flow.

📸 *[Screenshot: OWA login + mailbox view]*

---

## 🔹 Phase 3 — Tenant Prep + Entra Connect Sync
- Created Microsoft 365 tenant: **`weepwaap.onmicrosoft.com`**.
- Added UPN suffix to AD → updated users to `@weepwaap.onmicrosoft.com`.
- Installed **Entra Connect Sync** on DC01.
- Configured **Password Hash Sync**, OU filtering (`Lab Users`).
- Verified sync → users appeared in Entra ID with **Source = Windows Server AD**.
- Tested login with synced user (Alice Wong).

📸 *[Screenshot: Entra Admin Center showing synced users]*

---

## 🔹 Phase 4 — Hybrid Simulation
- Installed **Exchange Online PowerShell module**.
- Connected with:
  ```powershell
  Connect-ExchangeOnline -UserPrincipalName <GlobalAdminUPN>
