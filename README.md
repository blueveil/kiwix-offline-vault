# Kiwix Offline Vault

**Assembly Date:** 2026-08-15  
**ZIM Archive Date:** 2026-08  

A low-power, portable, off-grid knowledge server built on a Raspberry Pi Zero 2 W running Raspberry Pi OS Lite and `kiwix-serve`.

This project provides an offline Wi-Fi hotspot broadcasting archived web content (Wikipedia, Project Gutenberg, survival manuals, and pop-culture wikis) to any device with a web browser. It also includes direct local terminal fallbacks for monitor and keyboard usage, along with local media playback capabilities.

---

## Hardware Specifications & Cost Breakdown

| Component | Description | Cost (USD) |
| :--- | :--- | :--- |
| **Core Compute** | Raspberry Pi Zero 2 W (with blue aluminum heatsink) | $15.00 |
| **Storage** | 256GB MicroSD Card (SanDisk or Micro Center) | $25.00 |
| **Enclosure** | Clear acrylic case with acrylic standoffs | $6.00 |
| **Case & Shell** | Custom 3D-printed PETG hard case (~500g) with foam padding | $10.00 |
| **Power System** | 5V USB-C Power Supply with inline switch + USB-C to Micro-USB adapter | $10.00 |
| **Cables & Extras** | Mini-HDMI to HDMI cable, Micro-USB OTG cable, SD adapter | $15.00 |
| **Total Build Cost** | | **~$81.00** |

---

## System Architecture

```text
                      +-----------------------------------+
                      |   Raspberry Pi Zero 2 W          |
                      |   - Raspberry Pi OS Lite (Headless)|
                      |   - NetworkManager (AP Mode)      |
                      |   - kiwix-serve Systemd Service   |
                      +-----------------+-----------------+
                                        |
                 +----------------------+----------------------+
                 |                                             |
                 v                                             v
       [ Local Wi-Fi Access ]                        [ Direct Local Console ]
   - SSID: KiwixVault                              - Mini-HDMI Display Output
   - IP: 192.168.4.1:8080                          - Micro-USB OTG Keyboard Input
   - Accessible via Phone, Tablet, Laptop          - Terminal Browser: w3m
