# Pi-hole YouTube Blocklist (ABP)

A small [ABP-style](https://adblockplus.org/filter-cheatsheet) blocklist for Pi-hole to block YouTube at the DNS level—including on phones, tablets, and smart TVs.

Uses `||domain^` syntax, which blocks the domain and all of its subdomains.

## What it blocks

- `youtube.com` and all subdomains
- `youtu.be`
- `youtube-nocookie.com` (embedded players)
- `youtubekids.com`
- `googlevideo.com` (video streams; the key domain for stopping playback in apps and on TVs)
- `ggpht.com` / `ytimg.com` (thumbnails, static assets)
- `yt3.googleusercontent.com` (channel/avatar images)

This works across browsers, the YouTube mobile app, and TV/console apps because `googlevideo.com` carries the actual video streams and `youtubei.googleapis.com` (if you use the aggressive list) serves the app backend.

## What it does NOT do

- Does **not** bypass a client that uses its own DoH/DoT resolver (e.g., some browsers or newer Android/iOS apps with "Private DNS" enabled). If a device ignores Pi-hole for DNS, the block won't apply.
- Does **not** remove in-video ads that are served from the same domain as the video content.
- Blocking `googlevideo.com` can affect other Google video services on the same network.

## Install in Pi-hole (v6+)

1. Copy the **raw** URL of `youtube-blocklist.txt`, e.g.  
   `https://raw.githubusercontent.com/<user>/<repo>/main/youtube-blocklist.txt`
2. In Pi-hole, go to **Settings → Lists**.
3. Paste the raw URL into the **Address** field, add a comment if you like, and click **Add**.
4. Go to **Tools → Update Gravity** (or run `pihole -g`) to download the list.

Optional: repeat with `youtube-blocklist-aggressive.txt` if you want to also block the YouTube API endpoints (`youtubei.googleapis.com`, `yt.google.com`). This can help on some TV and mobile clients that fall back to the API when the main domains are blocked.

## Why ABP and not regex?

Pi-hole's **Lists** feature (subscribing to a URL) does **not** accept regex. It accepts normal domain entries and ABP-style `||domain^` entries. ABP syntax gives the same "domain + all subdomains" behavior as the regex approach, but in a single subscribable file.

## Notes

- Pi-hole applies these at the DNS level, so any device that uses Pi-hole for DNS is affected—phones and TVs included.
- Clear your client DNS cache after applying changes.
- Update gravity periodically to pick up changes.
- If a TV or phone still plays video, check that the device isn't using a hardcoded DNS server (e.g., 8.8.8.8) or Private DNS/DoH that bypasses Pi-hole.

## License

MIT
