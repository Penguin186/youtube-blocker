# Pi-hole YouTube Blocklist (Regex)

A small regex blocklist for Pi-hole to block YouTube domains at the DNS level.

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

## Install in Pi-hole

### Manual (all versions)

1. Open Pi-hole admin → **Settings → Domains** (or **Group Management → Domains**).
2. Choose **Regex** as the domain type and **Deny** as the action.
3. Paste each line from `youtube-regex.txt` as a separate entry.
4. Save and flush DNS (`pihole restartdns` or via the UI).

### Import by URL (Pi-hole v6+ Lists feature)

1. Copy the **raw** URL of `youtube-regex.txt`, e.g.
   `https://raw.githubusercontent.com/<user>/<repo>/main/youtube-regex.txt`
2. Add it under **Settings → Lists**, set the type to **Regex**, and update gravity.
3. If your Pi-hole version doesn't support regex lists by URL, use the manual method above.

### Aggressive list (optional)

Repeat the steps above with `youtube-regex-aggressive.txt` if you want to also block the YouTube API endpoints.

## Notes

- Pi-hole regex matching applies to the **domain name only**, not the full URL or path.
- Do not include `https://`, paths, or labels like `Regex deny` in the list files.
- Clear your client DNS cache after applying changes.

## License

MIT
