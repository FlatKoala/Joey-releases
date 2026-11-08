# Joey releases

Installation packages for **Joey**, the node-based media converter by
Koala Consulting: SDI, NDI, SRT, WebRTC, web graphics, clips and audio in
one graph, edited in the browser.

Joey is proprietary software; third-party licences are listed in
`/usr/share/doc/joey` after installation. This page is written by the
release build (`packaging/releases-README.md` in the Joey repository).

## Before you install

- Ubuntu 26.04 LTS on an x86-64 machine, ideally an Intel CPU with Quick
  Sync (integrated graphics) for H.264 and HEVC encoding.
- For SDI: install Blackmagic **Desktop Video** first, and update the
  cards' firmware if it asks (power the machine off fully afterwards).
- NDI and the Chromium runtime for web graphics come with the package.

## Install

Download the `.deb` of the newest release below, then:

    sudo apt install ./joey_<version>_amd64.deb

The installer creates the `joey` service user, enables the two services
(`joey-engine`, the media engine, and `joey-control`, the web interface)
and starts them. They start by themselves at every boot, with or without
anyone logged in, and restart after a crash. Every package is signed
(`.deb.asc`).

## Open Joey

In a browser on any machine on the same network:

    http://<address of the Joey machine>:8080

The installer prints the address. On the Joey machine itself, open
*Joey* from the application menu, or go to
`http://localhost:8080`. The user manual is at `/manual` on the same
address, and behind the **?** next to every node.

## Licence

Without a licence Joey runs in demo mode: everything works, each stream
runs for 10 minutes at a time and carries a watermark.

1. In Joey, open **License** and click **Download activation request**.
2. Send that file to Koala Consulting (toni@koalaconsulting.it).
3. Import the licence file you get back on the same page, with
   **Import licence file** or by pasting its text.

## Updates

Installed Joeys look here for new releases. **License** shows when one is
available and installs it with one click (signature checked first);
**Roll back** returns to the previous version. Manually: install the new
`.deb` the same way as above. Projects and settings are kept.

## Good to know

    systemctl status joey-engine joey-control     # are the services running?
    journalctl -u joey-engine -b                  # the engine's log since boot
    sudo systemctl restart joey-engine            # restart the media engine

- Projects and settings live in `/var/lib/joey`.
- **Display Out**: use *Direct (KMS)* mode. *Window* mode needs a desktop
  session, which the service does not have.
- For realtime work, run the machine without a remote desktop session
  open: its screen encoder competes with Joey for CPU and GPU.

## Uninstall

    sudo apt remove joey      # removes Joey, keeps projects and settings
    sudo apt purge joey       # also removes /var/lib/joey and the joey user

## Support

Koala Consulting · toni@koalaconsulting.it
