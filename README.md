# Enterprise Office Network Project




---

### 🛠️ Build Log & Issues Resolved

| Stage | Issue / Symptom | Root Cause | Resolution |
| :--- | :--- | :--- | :--- |
| **Stage 1: Core Server Room** | Dual uplinks from `Core-Router` to both `Switch-F1` and `Switch-F2` | Connecting two Layer 3 router interfaces into the same Layer 2 switch domain creates gateway conflicts | Removed the extra `Core-Router` $\rightarrow$ `Switch-F2` link so `Switch-F2` routes via `Switch-F1` (`192.168.2.1`), freeing `GigabitEthernet0/1` for Server Room B |
| **Stage 1: Core Server Room** | First cross-subnet ping from `DC01` to `DC02` timed out (`25% loss`) | Initial ARP resolution pause while the router learned `DC02`'s MAC address | Re-tested ICMP ping once ARP tables populated; verified `0%` packet loss and DNS resolution (`fs01.office.local`) |

> 📋 **Full Build History:** See [BUILDLOG.md](./BUILDLOG.md) for stage-by-stage progress notes, screenshots, and full troubleshooting walkthroughs.
