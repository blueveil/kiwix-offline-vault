# Kiwix Offline Vault

An affordable, self-contained, and low-power offline knowledge base project using a Raspberry Pi Zero 2 W, housed in a 3D-printed hard shell. Preserves Wikipedia, Project Gutenberg, and emergency reference archives with zero internet required.

- **Assembled:** 2026-08-15
- **ZIM Archive Date:** 2024-06 to 2026-08
- **Storage Used:** 211GB of archives on a 256GB card (229GB usable)

![Kiwix Vault Open](images/case-open.jpg)

---

## Overview

This project is a standalone offline digital library that serves curated `.zim` archives (Wikipedia, medical/survival databases, literature, etc.) to any device on the same local Wi-Fi network. For cost and how it compares to similar projects, see Project Goal and How It Compares below.

Unlike heavy off-grid platforms or expensive proprietary prepper drives, this project focuses on:
- **Minimal Power Consumption:** Runs on a 5V USB power supply or portable battery bank using a Raspberry Pi Zero 2 W.
- **Small Footprint:** Everything fits in a 3D-printed PETG storage case, along with a laminated lid-mounted reference guide.
- **Access:** Any smartphone, tablet, or laptop on the same Wi-Fi network as the Pi can open `http://kiwix.local:8080` (or `http://<PI-IP>:8080` if the name does not resolve). No internet connection is needed, only a local network.

---
## Project Goal

The goal of this build is to be as affordable as possible while still being a useful offline library. At about $81, including the power supply, cables and printed case, it costs less than every pre-built option I found that can actually be ordered today. Every part was chosen as the cheapest one that works: a Raspberry Pi Zero 2 W, a microSD card instead of an SSD, an acrylic case, and a 3D-printed box. Features that cost more (a built-in battery, an SSD, a faster board) are left out on purpose and listed under Future Roadmap & Upgrades as a separate project.

The one cheaper listing is the Wikimedia store's Internet-in-a-Box at $58. It is listed as sold out, it does not include a power supply, and ordering one through its partner costs more (see below). It also uses the same core hardware as this build, which is a good sign for the design.

---

## How It Compares

Similar projects exist. Most are more capable and more expensive, and one (the Wikimedia Internet-in-a-Box) uses the same hardware. Prices were checked on 2026-10-17 and change often.

| Project | What it is | Hardware | Approx. cost | Own Wi-Fi | Max users |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **This project** | DIY `kiwix-serve` on a Pi | Pi Zero 2 W, 256GB microSD | ~$81 total, with power supply and cables | No, joins an existing network | Not tested <!-- TODO: add the load test result --> |
| **Internet-in-a-Box, pre-built** | Assembled unit from the Wikimedia store and Wiki Project Med Foundation | Pi Zero 2 W, 256GB microSD, 3D-printed case | $58 listed (sold out); $83 outside the US or $124.50 in the US when ordered from the partner; no power supply | Yes | 10 (listing) |
| **Kiwix Hotspot** | Official pre-built device from Kiwix | Pi 5 (4GB), 256GB NVMe SSD, metal case | $300 (bundles $319 to $399) | Yes | Up to 24 |
| **PrepperDisk** | Pre-built Pi device, or software on an SD card for your own Pi | Pi-based, 256GB or 512GB | ~$200 to $280 (software card alone $165) | Yes | About 20 |
| **Internet-in-a-Box (IIAB), software** | Free software stack you install yourself | Raspberry Pi, or a PC running Linux | Free, plus your hardware | Yes | Up to 32 Wi-Fi clients on a Pi 4 or 5; its FAQ claims 32 on a Zero 2 W |
| **Project NOMAD** | Free software server with optional local AI | x86 PC running Ubuntu or Debian (not a Pi) | Free, plus your hardware | Serves your existing network | Depends on hardware |
| **RACHEL 5** | Pre-built education server from World Possible | 440GB SSD, built-in battery | $500 | Yes | 20 to 50 |

The $124.50 US price for the Internet-in-a-Box includes a 50% surcharge for tariffs, according to the ordering page. The base unit is $68 plus $15 shipping.

### Notes On Each

- **Internet-in-a-Box, pre-built:** The closest match to this build: a Raspberry Pi Zero 2 W with a 256GB microSD card in a 3D-printed case. It differs in four ways. It broadcasts its own Wi-Fi network, it ships assembled with English and Spanish Wikipedia, MDWiki and low-resolution maps, it lists support for 10 users, and it leaves out the power supply. Without the power supply and cables ($25), the parts in this build come to $56, about the same as the $58 listing. This build has a broader mix of content and includes everything needed to run it.
- **Kiwix Hotspot:** The closest relative, built on the same Kiwix software I use. It is plug-and-play, draws about 4 to 9 watts, and has an admin panel for adding content. It costs about 3.7 times as much as this build.
- **PrepperDisk:** Focused on preppers, with Wikipedia, maps, WikiHow, medical references, Project Gutenberg, iFixit and survival books. Sources disagree on the exact Pi model, so check before buying.
- **IIAB, software:** Runs a much larger set of apps than a single `kiwix-serve` service, including nearly 40 apps and optional learning platforms such as Kolibri, Moodle and Nextcloud, so it is a bigger setup. It installs on a Raspberry Pi, or on a Linux PC. I have not tried installing it myself.
- **Project NOMAD:** Free and open source (Apache 2.0). It bundles Kiwix, maps and Kolibri courses, with an optional AI assistant that runs locally. It is built for a standard PC, not a Raspberry Pi, and the full library fits comfortably on a 1TB drive.
- **RACHEL 5:** Aimed at schools and classrooms, with Khan Academy content and a teacher upload portal. The vendor says it is not meant to stay plugged in constantly.

### This Build vs the IIAB Software

This build runs one service, `kiwix-serve`, plus `w3m` as a local fallback. The IIAB software wraps the same kind of content in a larger system.

| | This build | IIAB software |
| :--- | :--- | :--- |
| Content server | `kiwix-serve` on port 8080 | Kiwix behind an NGINX proxy, plus other apps |
| Hotspot and network tools | None, joins an existing network | Built in (`iiab-hotspot-on`, `iiab-network`, `iiab-test-wifi`) |
| Admin | Terminal and plain-text guides | Web admin console |
| Extra apps | None | Kolibri, Moodle, Calibre-Web, Nextcloud and more |
| Captive portal and short address | `kiwix.local` or the Pi's IP | `box`, `box.lan` or `10.10.10.10`, with an optional captive portal |
| Setup effort | Low: a service file and some guides | Higher: a one-line installer, then configuration |
| Memory | Light | Fine on 512MB for static content; its FAQ recommends 2 to 4GB for heavy use |

IIAB's own FAQ says the Zero W and Zero 2 W "work great as learning kiosks, despite their meager 512MB RAM." That supports the hardware choice here.

### Hotspot Option

This build currently joins an existing Wi-Fi network, so it needs a router or a phone hotspot nearby. The Pi's Wi-Fi chip lists access point mode as supported (checked with `iw list`), so it should be able to act as its own hotspot, and the Wikimedia Internet-in-a-Box does the same on a Pi Zero 2 W. I have not set it up on this build. Things to know before switching:
- SSH over Wi-Fi to the Pi would stop working while it is a hotspot. Management would need a screen and keyboard, or a connection through the hotspot itself.
- The address changes. `kiwix.local` may or may not resolve, so a fixed address on the hotspot would be the safe choice.
- Reports of the plain `nmcli device wifi hotspot` command on a Zero 2 W are mixed. A persistent access point profile is reported to work on Raspberry Pi OS Bookworm.
<!-- TODO: after testing on the Pi, replace this section with the result and the exact steps that worked. -->

### Capacity

How many people can read at once is not tested on this build. What is known:

- The Wikimedia Internet-in-a-Box lists 10 simultaneous users on the same board and card size, without saying why.
- The IIAB FAQ says a Zero (2) W "is able to serve 32 students simultaneously" and that the hotspot on a Pi 4 or 5 supports up to 32 Wi-Fi clients. That is a claim in a FAQ, not a published test.
- The FAQ names many people running full-text searches of Wikipedia at the same time as the heavy case. Reading articles is much lighter than searching.
- This build serves devices through a router, so the router handles the Wi-Fi connections. My expectation is that the Pi's CPU, memory and SD card speed set the limit instead, but I have not tested that.
- At idle the whole system used about 127MB of the roughly 424MB of RAM available to it, with no swap in use.
<!-- TODO: add the load test result: how many devices, what they did, search times, peak memory and CPU. -->

### What This Project Gives Up

- No built-in battery, SSD, or admin panel.
- Fewer simultaneous users than the larger pre-built options, most likely. The Wikimedia unit lists 10 on the same Pi Zero 2 W, which is a reasonable ceiling to expect.
- No hotspot at the moment, so it needs a router or similar network nearby. The Pi's Wi-Fi supports access point mode, but I have not set it up.
- No support or warranty. The setup and fixes are on you.
- The $81 does not include the Wi-Fi network you connect through.

### What It Gives You

- A low cost that includes everything: power supply with a switch, cables, adapters and case. The Wikimedia unit leaves out the power supply, and ordering one costs $83 outside the US and $124.50 in the US.
- A setup you can fully understand: one web server, one service file, plain-text guides.
- A broader mix of content than the starter set: repair guides, emergency references, Project Gutenberg books, and more.
- Very low power use, which suits a USB power bank.
- A starting point you can grow: the same ZIM files work on Kiwix Hotspot, a Pi 5, or a mini PC if you outgrow the Zero 2 W.

### Sources

- [Internet-in-a-Box](https://internet-in-a-box.org/)
- [Internet-in-a-Box, Wikimedia Store listing](https://store.wikimedia.org/products/internet-in-a-box)
- [Internet-in-a-Box, ordering from Wiki Project Med Foundation](https://mdwiki.org/wiki/WikiProjectMed:Internet-in-a-Box/Buy)
- [IIAB FAQ](https://wiki.iiab.io/go/FAQ)
- [Kiwix Hotspot](https://get.kiwix.org/en/solutions/hotspots/kiwix-hotspot/)
- [PrepperDisk Premium software](https://www.prepperdisk.com/products/premium-software-on-pre-loaded-sd-card)
- [PrepperDisk pricing article (AOL)](https://www.aol.com/articles/offline-survival-library-fits-pocket-021700723.html)
- [Internet-in-a-Box installer page](https://d.iiab.io/README.html)
- [Project NOMAD FAQ](https://www.projectnomad.us/faq)
- [Personal Codex](https://personal-codex.com)
- [RACHEL 5](https://worldpossible.org/products/rachel-5-500)

---

## Hardware Specifications & Cost Breakdown

| Component | Description | Cost (USD) |
| :--- | :--- | :--- |
| **Computer** | Raspberry Pi Zero 2 W | $15.00 |
| **Storage** | 256GB Micro Center MicroSD Card | $25.00 |
| **Case** | Clear acrylic case with acrylic standoffs | $6.00 |
| **Box/Container** | Customized 3D-printed PETG hard case (~500g) with foam padding | $10.00 |
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

1. Flash Raspberry Pi OS Lite (32-bit, Debian 13 “trixie”) to the MicroSD card (user `librarian`, hostname `kiwix`, Wi-Fi configured).
2. Manually install the Kiwix tools (kiwix-tools 3.8.2, libkiwix 14.2.0, libzim 9.5.0). `kiwix-serve` and `kiwix-manage` live in `/usr/local/bin`.
3. Download the ZIM files from the Kiwix [library](https://library.kiwix.org) into `~/kiwix-library`.
4. Build the library index with `kiwix-manage` (see Re-indexing Library below).
5. Run `kiwix-serve` as a systemd service on port 8080 so it starts at boot.
6. Add the plain-text guides to the home directory (see Onboard Software & Guides above).

The service file, `/etc/systemd/system/kiwix.service`:

```ini
[Unit]
Description=Kiwix Offline Server
After=network.target

[Service]
Type=simple
User=librarian
ExecStart=/usr/local/bin/kiwix-serve --port=8080 --library /home/librarian/kiwix-library/library.xml
Restart=always
RestartSec=5
TimeoutStartSec=180

[Install]
WantedBy=multi-user.target
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
- **SD Card Image Clone:** Full .img backup images can be created using Win32DiskImager (Windows) or ApplePi-Baker (Mac) and compressed into .7z archives for long-term storage. The raw image is the size of the whole card, and because ZIM files are already compressed, expect the archive to stay close to the 213GB of used data.

---

## Notes & Limitations

- **Network:** Needs a local Wi-Fi network (such as a home router) for other devices to reach it, but no internet connection.
- **Project Gutenberg in w3m:** Hard to navigate in the terminal browser. See "Bypassing JavaScript-Heavy Landing Pages" above.
- **Power Off:** Always run `sudo shutdown -h now` and wait for the green LED to stop blinking before cutting power. The inline switch cuts power instantly and can corrupt the SD card.
- **Performance:** The Pi Zero 2 W has 512MB of RAM and 2.4GHz Wi-Fi only, so expect slow search with several users at once.
- **SD Card Wear:** SD cards degrade over years. Keep a cloned image backup.
- **Gutenberg Coverage:** The Project Gutenberg collection is a subset of the full library.
- **Archive Dates:** The ZIM files have different dates, from 2024-06 to 2026-08.
- **Storage:** The card is about 98% full (6.6GB free), so there is little room for more content or large updates.
- **Memory:** About 424MB of the Pi's 512MB is usable. At idle the whole system used about 127MB (measured with `free -h`).

---

## Future Roadmap & Upgrades

**Physical Enclosure & Hardware**
- **New Storage Case:** Reprint or choose a new design for the outer PETG hard shell to optimize internal component fit and durability.
- **Integrated Battery:** Explore adding an off-the-shelf or custom Li-ion battery bank for true portable power-on capability.

**Separate, More Expensive Project**
- **Computing & Storage Upgrade:** Transition to a better computer (such as a Raspberry Pi 5 or a low-power x86 Mini PC) with M.2 NVMe or SATA SSD storage for significantly higher read speeds, improved data retention, and superior endurance against corruption. This would also allow running full graphical local browsers, indexing larger libraries, and hosting multi-user concurrent sessions effortlessly. The Zero 2 W has no PCIe, so this is a new build rather than an upgrade, and the goal of this one is to stay as cheap as possible.

---

## Attribution

- [Kiwix](https://kiwix.org) provides the server software and the ZIM archives.
- Content comes from Wikipedia and the other Wikimedia projects, Project Gutenberg, iFixit, Appropedia, PhET, MedlinePlus, Ready.gov, FAS IRP, the USDA, WikiVet, MDWiki, Corey Schafer, and the Minecraft, Pokémon, Stardew Valley, and League of Legends wikis.
- Each ZIM keeps its own license and attribution. Check each file on the Kiwix [library](https://library.kiwix.org).
- This repo does not include or redistribute any ZIM files.
- **Case:** [Snaplock V3](https://makerworld.com/en/models/2168356-snaplock-v3) by [Hugo](https://makerworld.com/en/@Hugo) on MakerWorld, licensed under the MakerWorld Exclusive License. Printed in PETG using the model's customizer with these inside dimensions: [W x L x H mm, corner radius]. The model files are not included here; download them from MakerWorld.

---

## License

The documentation in this repo is under the MIT License (see [LICENSE](LICENSE)). The archived content keeps its own licenses.
