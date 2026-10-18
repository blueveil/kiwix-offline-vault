================================================================================
KIWIX OFFLINE LIBRARY (RASPBERRY PI ZERO 2 W)
================================================================================

*** HOW TO READ THIS FILE ***
- SCROLL UP/DOWN : Use Up Arrow / Down Arrow or Page Up / Page Down
- EXIT TO PROMPT : Press 'q' on your keyboard to close this viewer

================================================================================

This Raspberry Pi acts as a portable, offline Wikipedia and digital library hosting
over 200 GB of information (encyclopedias, medical guides, literature, repair
manuals, maps, textbooks, and simulations).

An internet connection is NOT required. Traffic stays strictly on local Wi-Fi.

[ DIRECTORY MAP ]
--------------------------------------------------------------------------------
/home/librarian/kiwix-library : Main folder storing all 25+ ZIM knowledge archives
/usr/local/bin/               : Location of Kiwix binaries (kiwix-serve, kiwix-manage)
/etc/systemd/system/          : System directory holding kiwix.service configuration
/etc/NetworkManager/          : Directory holding Wi-Fi network profiles

[ SYSTEM ARCHITECTURE & COMPONENTS ]
--------------------------------------------------------------------------------
PRIMARY USER    : librarian
DEFAULT PORT    : 8080 (Standard non-root HTTP web server port)
ZIM FILES       : Highly compressed single-file web archives (.zim)
LIBRARY MANIFEST: library.xml file generated to index all 200GB+ of ZIMs at once
KIWIX SERVER    : Binary (kiwix-serve) that reads ZIM files and serves web pages
SYSTEMD SERVICE : Background process (kiwix.service) running automatically on boot

[ HOW TO ACCESS THE SERVER (EVERYDAY USE) ]
--------------------------------------------------------------------------------
1. Connect your phone, tablet, or computer to the same Wi-Fi network as the Pi.

2. Open any web browser (Chrome, Safari, Firefox, Edge, Brave).

3. Type either address into your browser address bar and hit Enter:

   http://kiwix.local:8080

   OR check current local IP (run 'hostname -I' on the Pi):
   http://<YOUR-PI-IP>:8080  (Example: http://192.168.1.50:8080)

   (Note: If kiwix.local fails to load, your router lacks local mDNS support;
   use the IP address method instead.)

[ MOVING TO A NEW WI-FI NETWORK ]
--------------------------------------------------------------------------------
1. Attach a display to Mini-HDMI and a keyboard to the Micro-USB OTG port.
2. Scan nearby Wi-Fi networks : sudo nmcli device wifi list
3. Connect to new network     : sudo nmcli device wifi connect "SSID" password "PASSWORD"
4. Check new assigned IP      : hostname -I

[ MANAGING & REINDEXING THE LIBRARY ]
--------------------------------------------------------------------------------
Whenever new .zim files are added or deleted, regenerate the XML library index:

cd ~/kiwix-library && rm -f library.xml && for f in *.zim; do kiwix-manage library.xml add "$f"; done
sudo systemctl restart kiwix.service

[ NO-WIFI / EMERGENCY BACKUP ACCESS ]
--------------------------------------------------------------------------------
If Wi-Fi is unavailable, browse the library directly using an attached screen
and keyboard. The Kiwix server starts by itself at boot, so there is nothing
to start by hand.

1. Power OFF the Pi. Connect the display to the Mini-HDMI port BEFORE powering
   on. The Pi may not detect a screen that is plugged in later.
2. Plug the Micro-USB OTG cable into the port labeled USB (NOT the port
   labeled PWR IN), then plug the keyboard into the OTG cable.
3. Power on and wait about 60 seconds for the login prompt.
4. Log in as 'librarian' with the password you set.
5. Open the library in the text browser (w3m is preinstalled):
   w3m http://localhost:8080
6. If the page does not load, check the server:
   sudo systemctl status kiwix.service
7. When finished, shut down and wait for the green LED to stop blinking
   before cutting power:
   sudo shutdown -h now

PROJECT GUTENBERG TIP: Its landing page may not display in w3m. Press
Shift + U, type http://localhost:8080/content/ and press Enter. Then press /
to search the list.

[ COMMON TROUBLESHOOTING & UTILITIES ]
--------------------------------------------------------------------------------
CHECK SERVICE STATUS : sudo systemctl status kiwix.service
RESTART SERVER       : sudo systemctl restart kiwix.service
STOP SERVER          : sudo systemctl stop kiwix.service
VIEW LIVE LOGS       : sudo journalctl -u kiwix.service -n 20 --no-pager
SAFE SHUTDOWN        : sudo shutdown -h now

[ LOG ]
--------------------------------------------------------------------------------
LAST UPDATED     : 2026-10-17
