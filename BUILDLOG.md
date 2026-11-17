# 📋 Enterprise Office Network — Build & Troubleshooting Log

Stage-by-stage progress notes, configuration milestones, and troubleshooting fixes encountered while building the multi-floor office topology in Cisco Packet Tracer.

---

### ✅ Stage 1 Complete — Core Server Infrastructure (`192.168.2.0/24` & `192.168.3.0/24`)
* **Completed:** Wired `Core-Router` to Server Room A (`Switch-F1`, `Switch-F2`) and Server Room B (`Switch-F3`). Configured static IPs across all 5 servers (`DC01`, `FS01`, `EX01`, `DC02`, `PRT01`) and enabled DNS (`office.local`), FTP (`staff1` and `admin` accounts), and SMTP/POP3 mail services.
* **Verified:** Cross-subnet ICMP ping from `DC01` to `DC02` and hostname DNS resolution (`ping fs01.office.local`).
* **Issues Logged:**
  * **Redundant router uplink:** Removed duplicate cable between `Core-Router` and `Switch-F2` to prevent Layer 2/Layer 3 gateway conflicts and free `GigabitEthernet0/1` for Server Room B.
  * **Initial cross-subnet ping timeout:** First ICMP packet between `DC01` and `DC02` timed out while ARP tables resolved MAC addresses; subsequent packets replied with 0% loss.

---

### ✅ Stage 2: Wireless Network & DHCP Relay Integration (Completed)
- **Objective:** Extend the enterprise topology to support wireless clients (`192.168.10.0/24`) with secure WPA2 authentication, dynamic IP leasing via DHCP, and inter-vlan/subnet routing.
- **Implementation:**
  - Added `Switch-Wireless` connected to `Core-Router` (`GigabitEthernet0/2`, IP: `192.168.10.1`).
  - Deployed autonomous Access Points (`Lobby-AP` and `Cafe-AP`) secured with WPA2-PSK (`Wifi1234`) and SSIDs `Office-Lobby` and `Office-Cafe`.
  - Swapped laptop physical NICs to wireless cards (`WPC300N`) and successfully associated both clients.
  - Configured DHCP Scope `WirelessPool` (`192.168.10.50+`) on `DC01` (`192.168.2.10`).
  - Configured `ip helper-address 192.168.2.10` on `Core-Router` GE0/2 to forward cross-subnet DHCP requests.
- **Verification:** Laptops successfully leased IPs (`192.168.10.50` and `192.168.10.51`) and verified full cross-subnet ping connectivity to core servers.

---
