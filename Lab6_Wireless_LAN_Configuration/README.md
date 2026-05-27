# Lab 6 – Configuring and Securing a Wireless LAN

## Objective
Configure and secure a Wireless Access Point (WAP) in Cisco Packet Tracer, covering IP addressing, SSID setup, WPA2 encryption, MAC filtering, DHCP reservations, and guest network configuration.

---

## Part 1 – Initial Setup & IP Configuration

Opened PC_A and ran `ipconfig /all` to check the initial state — the device had no address (0.0.0.0). Set PC_A to DHCP and it received **192.168.0.105 / 255.255.255.0** with a default gateway of **192.168.0.1**, which is also the WAP acting as the DHCP server.

Accessed the WAP admin GUI at `http://192.168.0.1` using the default credentials (admin/admin).

---

## Part 2 – WAP Network Reconfiguration (Subnetting)

**Fifth private Class B network:** 172.20.0.0  
**Borrowing 8 bits** creates **/24 subnets** — 256 subnets with 254 hosts each.

First 3 subnets:
1. 172.20.0.0 /24
2. 172.20.1.0 /24
3. 172.20.2.0 /24

Assigned the WAP the **first IP on the second subnet**: **172.20.1.1**

Configured the DHCP pool starting at the **15th address** with a max of **25 clients**:

| Setting | Value |
|---------|-------|
| Router IP | 172.20.1.1 |
| DHCP Start | 172.20.1.15 |
| DHCP End | 172.20.1.39 |
| Max Clients | 25 |

After saving, the browser timed out because the WAP's IP changed. Ran `ipconfig /renew` on PC_A and it received **172.20.1.105** on the new subnet.

---

## Part 3 – Wireless Network (SSID) Configuration

Configured three wireless networks on the WAP:

| Band | SSID | Broadcast |
|------|------|-----------|
| 2.4 GHz | WLAN24 | Disabled (hidden) |
| 5 GHz – 1 | WLAN51 | Enabled |
| 5 GHz – 2 | WLAN52 | Enabled |

- **Laptop_1** connected to WLAN24 via manual Config tab (SSID not broadcasting)
- **Laptop_2 & Laptop_3** connected to WLAN51
- **Laptop_4** connected to WLAN52
- Some laptops required the **PT-LAPTOP-NM-1W-AC** wireless module upgrade

---

## Part 4 – MAC Address Filtering

Created a MAC filter on the 2.4 GHz port set to **Permit** only listed devices.

- **Laptop_1 MAC:** 00:D0:FF:50:E5:B1
  - Block ID: 00:D0:FF
  - Device ID: 50:E5:B1

Added Laptop_1's MAC to the filter and verified it could still connect to WLAN24.

---

## Part 5 – DHCP Reservation

Created a DHCP reservation for Laptop_3 to always receive the same IP:

- **Laptop_3 MAC:** 00:E0:8F:50:5B:47
  - Block ID: 00:E0:8F
  - Device ID: 50:5B:47
- **Reserved IP:** 172.20.1.21 (6th address in the pool)
- **Reservation Name:** Admin Laptop

After running `ipconfig /renew` on Laptop_3, it received **172.20.1.21** as expected.

---

## Part 6 – WPA2 Security Configuration

Set all three wireless networks to **WPA2 Personal** with **AES** encryption:

| Network | Passphrase |
|---------|-----------|
| WLAN24 (2.4 GHz) | P@ssw0rd24 |
| WLAN51 (5 GHz – 1) | P@ssw0rd51 |
| WLAN52 (5 GHz – 2) | P@ssw0rd52 |

After saving, all laptops disconnected. Reconnected each by setting Authentication to **WPA2-PSK** (Pre-Shared Key) and entering the correct passphrase with AES encryption type. All laptops reconnected successfully.

Changed the WAP admin password to **cisco**.

---

## Part 7 – Guest Network

Configured a guest network on the 5 GHz – 1 band:

| Setting | Value |
|---------|-------|
| SSID | Guest50 |
| Broadcast SSID | Enabled |
| Security | WPA2 Personal / AES |
| Passphrase | Guest@50 |
| Guest isolation | Guests cannot see each other or access local network |

Connected the smartphone to the Guest50 network. All end devices confirmed connected to their respective wireless networks.

---

## Key Concepts Covered

- **SSID** (Service Set Identifier) — the name that identifies a wireless network
- **Hidden SSID** — clients can still connect by manually entering the network name and credentials
- **WPA2 Personal / AES** — current standard for wireless security; AES (Advanced Encryption Standard) is the preferred encryption method
- **PSK** (Pre-Shared Key) — a shared passphrase used for WPA2 Personal authentication
- **MAC Filtering** — allows or blocks devices based on their hardware MAC address
- **DHCP Reservation** — ensures a specific device always receives the same IP address

---

## Files

| File | Description |
|------|-------------|
| [`wireless_lan_configuration.pka`](./wireless_lan_configuration.pka) | Completed Packet Tracer topology |
| [`wireless_lan_worksheet.pdf`](./wireless_lan_worksheet.pdf) | Completed lab worksheet with all answers |
