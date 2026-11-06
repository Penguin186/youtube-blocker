# Pi-hole YouTube Blocklist (ABP)

A small [ABP-style](https://adblockplus.org/filter-cheatsheet) blocklist for Pi-hole to block YouTube at the DNS level.

Uses `||domain^` syntax, which blocks the domain and all of its subdomains.

## What it blocks

- `youtube.com` and all subdomains
- `youtu.be`
- `youtube-nocookie.com` (embedded players)
- `youtubekids.com`
- `googlevideo.com` (video streams)
- `ggpht.com` / `ytimg.com` (thumbnails, static assets)
- `yt3.googleusercontent.com` (channel/avatar images)

## What it does NOT do

- Does **not** bypass browser/app DoH or DoT. If a client uses encrypted DNS, Pi-hole is bypassed.
- Does **not** reliably block the YouTube mobile app or Smart TV apps, which often use hardcoded IPs or DoH.
- Blocking `googlevideo.com` can affect other Google video services.

## Install in Pi-hole (v6+)

1. Copy the **raw** URL of `youtube-blocklist.txt`, e.g.  
   `https://raw.githubusercontent.com/<user>/<repo>/main/youtube-blocklist.txt`
2. In Pi-hole, go to **Settings → Lists**.
3. Paste the raw URL into the **Address** field, add a comment if you like, and click **Add**.
4. Go to **Tools → Update Gravity** (or run `pihole -g`) to download the list.

Optional: repeat with `youtube-blocklist-aggressive.txt` if you want to also block the YouTube API endpoints.

## Why ABP and not regex?

Pi-hole's **Lists** feature (subscribing to a URL) does **not** accept regex. It accepts normal domain entries and ABP-style `||domain^` entries. ABP syntax gives the same "domain + all subdomains" behavior as the regex approach, but in a single subscribable file.

## Notes

- Pi-hole applies these at the DNS level, so anything resolved through Pi-hole is affected.
- Clear your client DNS cache after applying changes.
- Update gravity periodically to pick up changes.

## License

MIT
