# Kiwix Offline Vault

An affordable, self-contained, and low-power offline knowledge base project using a Raspberry Pi Zero 2 W, housed in a 3D-printed hard shell. Preserves Wikipedia, WikiHow, Project Gutenberg, and emergency reference archives with zero internet required.

- **Assembled:** 2026-08-15
- **ZIM Archive Date:** 2026-08

![Kiwix Vault Open](insert-image.jpg)

---

## Overview

This project is a standalone offline digital library designed to broadcast a localized Wi-Fi hotspot serving curated `.zim` archives (Wikipedia, medical/survival databases, literature, etc.). 

Unlike heavy off-grid platforms or expensive proprietary prepper drives, this project focuses on:
- **Minimal Power Consumption:** Runs on a 5V USB power supply or portable battery bank using a Raspberry Pi Zero 2 W.
- **Small Footprint:** Everything fits in a 3D-printed PETG storage case, along with a laminated lid-mounted reference guide.
- **Access:** Broadcasts an open Wi-Fi access point (`http://kiwix.local:8080`) accessible by any smartphone, tablet, or laptop.

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
- **Computer:** Raspberry Pi Zero 2 W with anodized blue aluminum heatsink in a clear acrylic case with standoffs.
- **Storage & OS:** MicroSD Card running Raspberry Pi OS Lite configured with `kiwix-serve`. Includes a full-size SD card adapter inside a protective micro jewel case.
- **Power:** 5V USB-C Power Supply with inline toggle switch, paired with a USB-C to Micro-USB adapter.
- **Display & IO:** Mini-HDMI to HDMI cable and Micro-USB OTG cable.
- **Enclosure:** 3D-printed dual-latch black hard shell with an internal foam pad and top-lid laminated reference guide attached via loop/hook Velcro.

---

## Onboard Software & Guides

The internal MicroSD card includes local plain-text documentation stored directly in the home directory (`~`) for terminal access via `less` or `cat`:

- `README.txt`: Network setup, Wi-Fi access steps, and console configurations.
- `QUICK_COMMANDS.txt`: Command cheat sheet for terminal web browsing (`w3m`), Wi-Fi management (`nmcli`), and safe shutdown (`sudo shutdown -h now`).
- `SPECS.txt`: Complete breakdown of hardware specs and software environment.

---

## Included ZIM Files

The onboard storage is split into two primary categories:

### Practical & Survival Knowledge
- **Wikipedia (Full Archive):** Comprehensive database covering medicine, chemistry, agriculture, history, and engineering.
- **Survival & DIY:** Specialized archives covering water purification, sanitation, WikiHow guides, and farming.
- **Project Gutenberg:** Thousands of public-domain literature titles, classic novels, and historical texts.

### Miscellaneous
- **Stardew Valley Wiki:** Farming schedules, crop yields, and crafting mechanics.
- **Pokémon Wiki:** Move sets, creature indices, and battle mechanics.
- **League of Legends Wiki:** Champion lore and statistical breakdowns.

---

## Terminal Browsing & Local Media Playback

When accessing the vault directly via a connected monitor and keyboard (without Wi-Fi clients), use lightweight command-line tools:

### Text Web Browsing (`w3m`)
```bash
w3m http://localhost:8080
```
---

## Bypassing JavaScript-Heavy Landing Pages

Some archives (such as Project Gutenberg) rely on JavaScript or dynamic menus on their landing pages that do not render natively in w3m.

- **Direct Content Listing:** To skip dynamic landing pages and access raw library archives, open w3m, press Shift + U, and navigate directly to:
```bash
http://localhost:8080/content/
```
- **In-Page Search:** Use the native w3m search function by pressing / to search through text lists directly on the screen.

---

## Backup & Maintenance

To protect against NAND flash charge leakage over multi-year dormant storage:
- **Periodic Refresh:** Power on the unit once every 1–2 years for a few minutes to refresh flash memory cells.
- **SD Card Image Clone:** Full .img backup images can be created using Win32DiskImager (Windows) or ApplePi-Baker (Mac) and compressed into .7z archives for long-term storage.

---

## Future Roadmap & Upgrades

**Physical Enclosure & Hardware**
- **New Storage Case:** Reprint or refine the outer PETG hard shell to optimize internal component fit and durability.
- **Integrated Battery:** Explore adding an onboard UPS (Uninterruptible Power Supply) HAT or custom 18650 Li-ion battery bank for true portable power-on capability.

**Hardware & Storage Architecture Upgrades**
- **Non-SD Storage Media: Upgrade from MicroSD card storage to an M.2 NVMe or SATA SSD via USB/PCIe HAT for significantly higher read speeds, improved data retention, and superior endurance against corruption.
- **SBC Upgrade: Transition to a higher-tier Single Board Computer (such as a Raspberry Pi 5 or a low-power x86 Mini PC) to allow running full graphical local browsers, indexing larger libraries, and hosting multi-user concurrent sessions effortlessly.
