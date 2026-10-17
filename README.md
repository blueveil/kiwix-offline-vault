# Kiwix Offline Vault

A self-contained, low-power offline knowledge base project using a Raspberry Pi Zero 2 W, housed in a 3D-printed hard shell. Preserves Wikipedia, WikiHow, Project Gutenberg, and emergency reference archives with zero internet required.

* **Assembled:** 2026-08-15
* **ZIM Archive Date:** 2026-08

![Kiwix Vault Open](insert-image.jpg)

---

## Overview

This project is a standalone offline digital library designed to broadcast a localized Wi-Fi hotspot serving curated `.zim` archives (Wikipedia, medical/survival databases, literature, and gaming lore). 

Unlike heavy off-grid platforms or expensive proprietary prepper drives, this project focuses on:
* **Minimal Power Consumption:** Runs on a 5V USB power supply or portable battery bank using a Raspberry Pi Zero 2 W.
* **Physical Integration:** Custom 3D-printed case, dedicated cable layout, clear acrylic Pi protection, and laminated lid-mounted reference sheets.
* **Zero-Friction Access:** Broadcasts an open Wi-Fi access point (`http://kiwix.local:8080`) accessible by any smartphone, tablet, or laptop.

---

## Hardware Specifications & Cost Breakdown

| Component | Description | Cost (USD) |
| :--- | :--- | :--- |
| **Computer** | Raspberry Pi Zero 2 W | $15.00 |
| **Storage** | 256GB Micro Center MicroSD Card | $25.00 |
| **Case** | Clear acrylic case with acrylic standoffs | $6.00 |
| **Box/Container** | Custom 3D-printed PETG hard case (~500g) with foam padding | $10.00 |
| **Power** | 5V USB-C Power Supply with inline switch + USB-C to Micro-USB adapter | $10.00 |
| **Cables & Extras** | Mini-HDMI to HDMI cable, Micro-USB OTG cable, SD adapter | $15.00 |
| **Total Build Cost** | | **~$81.00** |

---

## Hardware Layout

![Hardware Layout](insert-image.jpg)

### Enclosed Hardware & Components
* **Computer:** Raspberry Pi Zero 2 W with aluminum heatsink in a clear acrylic case with standoffs.
* **Storage & OS:** MicroSD Card running Raspberry Pi OS Lite configured with `kiwix-serve`. Includes a full-size SD card adapter inside a protective plastic case.
* **Power:** 5V USB-C Power Supply with inline toggle switch, paired with a USB-C to Micro-USB adapter.
* **Display & IO:** Mini-HDMI to HDMI cable and Micro-USB OTG cable.
* **Enclosure:** 3D-printed dual-latch hard shell with an internal foam pad and top-lid laminated reference guide.

---

## Onboard Software & Guides

The internal MicroSD card includes local plain-text documentation stored directly in the home directory for terminal access via `less`:

1. `README.txt`: Network setup, Wi-Fi access steps, and console configurations.
2. `QUICK_COMMANDS.txt`: Command cheat sheet for terminal web browsing (`w3m`), Wi-Fi management (`nmcli`), and safe shutdown (`sudo shutdown -h now`).
3. `SPECS.txt`: Complete breakdown of hardware specs and software environment.

---

## Included ZIM Files

The onboard storage is partitioned into two primary categories:

### 1. Practical
* **Wikipedia (Full Archive):** Comprehensive database covering medicine, chemistry, agriculture, history, and engineering.
* **Survival & DIY:** Specialized archives covering water purification, sanitation, and farming.
* **Project Gutenberg:** Thousands of public-domain literature titles and historical texts.

### 2. Culture & Entertainment
* **Stardew Valley Wiki:** Farming schedules, crop yields, and crafting mechanics.
* **Pokémon Wiki:** Move sets, creature indices, and game mechanics.
* **League of Legends Wiki:** Champion lore and statistical breakdowns.

---

## Backup & Maintenance

To protect against NAND flash charge leakage over multi-year dormant storage:
1. **Periodic Refresh:** Power on the unit once every 1–2 years for a few minutes to refresh flash memory cells.
2. **SD Card Image Clone:** Full `.img` backup images can be created using `Win32DiskImager` (Windows) or `ApplePi-Baker` (Mac) and compressed into `.7z` archives for long-term storage.
