# Kiwix Offline Vault

An affordable, self-contained, and low-power offline knowledge base project using a Raspberry Pi Zero 2 W, housed in a 3D-printed hard shell. Preserves Wikipedia, Project Gutenberg, and emergency reference archives with zero internet required.

- **Assembled:** 2026-08-15
- **ZIM Archive Date:** 2024-06 to 2026-08

![Kiwix Vault Open](images/case-open.jpg)

---

## Overview

This project is a standalone offline digital library that serves curated `.zim` archives (Wikipedia, medical/survival databases, literature, etc.) to any device on the same local Wi-Fi network.
<!-- TODO: confirm client mode vs hotspot after the Pi check (nmcli connection show). Update this paragraph and the Access bullet if it does broadcast its own Wi-Fi. -->

Unlike heavy off-grid platforms or expensive proprietary prepper drives, this project focuses on:
- **Minimal Power Consumption:** Runs on a 5V USB power supply or portable battery bank using a Raspberry Pi Zero 2 W.
- **Small Footprint:** Everything fits in a 3D-printed PETG storage case, along with a laminated lid-mounted reference guide.
- **Access:** Any smartphone, tablet, or laptop on the same Wi-Fi network as the Pi can open `http://kiwix.local:8080` (or `http://<PI-IP>:8080` if the name does not resolve). No internet connection is needed, only a local network.

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

![Hardware Layout](images/hardware-layout.jpg)

### Enclosed Hardware & Components
- **Computer:** Raspberry Pi Zero 2 W with anodized blue aluminum heatsink in a clear acrylic case with standoffs.
- **Storage & OS:** MicroSD Card running Raspberry Pi OS Lite configured with `kiwix-serve`. Includes a full-size SD card adapter inside a protective micro jewel case.
- **Power:** 5V USB-C Power Supply with inline toggle switch, paired with a USB-C to Micro-USB adapter.
- **Display & IO:** Mini-HDMI to HDMI cable and Micro-USB OTG cable.
- **Enclosure:** 3D-printed dual-latch black hard shell with an internal foam pad and top-lid laminated reference guide attached via loop/hook Velcro.

---

## Case

A dual-latch 3D-printed PETG hard shell with foam padding. The design I used, my resized version, and the print notes are in [`case/`](case/).

---

## Onboard Software & Guides

The internal MicroSD card includes local plain-text documentation stored directly in the home directory (`~`) for terminal access via `less` or `cat`:

- `README.txt`: Network setup, Wi-Fi access steps, and console configurations.
- `QUICK_COMMANDS.txt`: Command cheat sheet for terminal web browsing (`w3m`), Wi-Fi management (`nmcli`), and safe shutdown (`sudo shutdown -h now`).
- `SPECS.txt`: Complete breakdown of hardware specs and software environment.

Copies of these files are in [`onboard/`](onboard/). A printed one-page version of the guide is mounted inside the case lid: [`case/printed_guide.txt`](case/printed_guide.txt).

---

## Included ZIM Files

The onboard storage contains a broad array of practical survival databases, educational tools, repair references, and more. The full list with file names, descriptions, and versions is in [ZIMS.md](ZIMS.md).

### Practical & Survival Knowledge
- **Wikipedia (Full Archive):** Comprehensive database covering medicine, chemistry, agriculture, history, and engineering.
- **Medical & Emergency Reference:** MedlinePlus, MDWiki, Wikivet, IRP FAS Military Medicine, and Ready.gov.
- **Survival, Repair & DIY:** Appropedia (sustainable tech), iFixit repair guides, USDA 2015 database, and ZIMgit guides (Food Preparation, Knots, Water).
- **Project Gutenberg:** Multi-part LCC library archives containing thousands of classic literature titles, historical texts, and foundational books.

### STEM & Education
- **PhET Interactive Simulations:** Science and mathematics simulation tools.
- **Corey Schafer Python Tutorials:** Offline programming guides and references.
- **Wiktionary & Wikivoyage:** Offline multi-language dictionary and global travel/geography guides.

### Culture, Maps & Gaming Lore
- **US Maps Archive:** Offline geography and topographical reference.
- **Gaming Wikis:** Stardew Valley Wiki, Pokémon Wiki, Minecraft Wiki, and League of Legends Wiki.

---

## How It Was Built

The setup is simple: install an OS, add a web server, copy in the archives, and write some plain-text guides.

1. Flash Raspberry Pi OS Lite to the MicroSD card (user `librarian`, hostname `kiwix`, Wi-Fi configured).
2. Install the Kiwix tools. `kiwix-serve` and `kiwix-manage` live in `/usr/local/bin`.
3. Download the ZIM files from the [Kiwix library](https://library.kiwix.org) into `~/kiwix-library`.
4. Build the library index with `kiwix-manage` (see Re-indexing Library below).
5. Run `kiwix-serve` as a systemd service on port 8080 so it starts at boot.
6. Add the plain-text guides to the home directory (see Onboard Software & Guides above).
<!-- TODO: note how the Kiwix tools were installed (release download or apt) and the version from `kiwix-serve --version`. -->

The service file, `/etc/systemd/system/kiwix.service`:

```ini
# TODO: paste the output of: cat /etc/systemd/system/kiwix.service
```

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

## Re-indexing Library
Whenever new ZIM files are added or deleted, regenerate the XML library index:
```bash
cd ~/kiwix-library && rm -f library.xml && for f in *.zim; do kiwix-manage library.xml add "$f"; done && sudo systemctl restart kiwix.service
```

---

## Backup & Maintenance

To protect against NAND flash charge leakage over multi-year dormant storage:
- **Periodic Refresh:** Power on the unit once every 1–2 years for a few minutes to refresh flash memory cells.
- **SD Card Image Clone:** Full .img backup images can be created using Win32DiskImager (Windows) or ApplePi-Baker (Mac) and compressed into .7z archives for long-term storage.

---

## Notes & Limitations

- **Network:** Needs a local Wi-Fi network (such as a home router) for other devices to reach it, but no internet connection.
- **Project Gutenberg in w3m:** Hard to navigate in the terminal browser. See "Bypassing JavaScript-Heavy Landing Pages" above.
- **Power Off:** Always run `sudo shutdown -h now` and wait for the green LED to stop blinking before cutting power. The inline switch cuts power instantly and can corrupt the SD card.
- **Performance:** The Pi Zero 2 W has 512MB of RAM and 2.4GHz Wi-Fi only, so expect slow search with several users at once.
- **SD Card Wear:** SD cards degrade over years. Keep a cloned image backup.
- **Gutenberg Coverage:** The Project Gutenberg collection is a subset of the full library.
- **Archive Dates:** The ZIM files have different dates, from 2024-06 to 2026-08.
<!-- TODO: add boot time (power-on to a loading page) and any other measurements from the Pi test. -->

---

## Future Roadmap & Upgrades

**Physical Enclosure & Hardware**
- **New Storage Case:** Reprint or refine the outer PETG hard shell to optimize internal component fit and durability.
- **Integrated Battery:** Explore adding an onboard UPS (Uninterruptible Power Supply) HAT or custom 18650 Li-ion battery bank for true portable power-on capability.

**Separate, More Expensive Project**
- **Computing & Storage Upgrade:** Transition to a better computer (such as a Raspberry Pi 5 or a low-power x86 Mini PC) with M.2 NVMe or SATA SSD storage for significantly higher read speeds, improved data retention, and superior endurance against corruption. This would also allow running full graphical local browsers, indexing larger libraries, and hosting multi-user concurrent sessions effortlessly. The Zero 2 W has no PCIe, so this is a new build rather than an upgrade, and the goal of this one is to stay as cheap as possible.

---

## Attribution

- [Kiwix](https://kiwix.org) provides the server software and the ZIM archives.
- Content comes from Wikipedia and the other Wikimedia projects, Project Gutenberg, iFixit, Appropedia, PhET, MedlinePlus, Ready.gov, FAS IRP, the USDA, WikiVet, MDWiki, Corey Schafer, and the Minecraft, Pokémon, Stardew Valley, and League of Legends wikis.
- Each ZIM keeps its own license and attribution. Check each file on the [Kiwix library](https://library.kiwix.org).
- This repo does not include or redistribute any ZIM files.
- **Case:** [Snaplock V3](https://makerworld.com/en/models/2168356-snaplock-v3) by [Hugo](https://makerworld.com/en/@Hugo) on MakerWorld, licensed under the MakerWorld Exclusive License. Printed in PETG using the model's customizer with these inside dimensions: [W x L x H mm, corner radius]. The model files are not included here; download them from MakerWorld.

---

## License

The documentation in this repo is under the MIT License (see [LICENSE](LICENSE)). The archived content keeps its own licenses.
