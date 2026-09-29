# Job tracker

Single-file HTML · Vanilla JS · No build, no dependencies · Fully offline

## Status

- App: done
- Storage: done
- Offline: done

## Spec

- Data: everything lives in `jobs.json`; nothing is stored in the page or the browser
- Categories: up to 4 user-named tracks (e.g. Industry, PhD, Part-time)
- Structure: category → organisation → roles
- Role fields: role, contact, status, applied on, URL, location, notes
- Statuses: Not applied, Applied, Interview, Processing, Accepted, Rejected, Dropped
- Applied on: filled with today's date the first time a role is set to Applied (editable)
- Saving: `⌘S` / `Ctrl+S` writes back to the same file (File System Access API); falls back to import/export JSON in other browsers
- Migration: older `jobs.json` files are upgraded automatically on open

## Privacy

The page makes no network requests of its own.

- No external fonts, scripts, styles or images. Fonts come from the system; IBM Plex is used if it is installed (`sudo apt install fonts-ibm-plex`), otherwise the system font.
- A Content Security Policy in the page blocks any request to another address, so an edit that adds one later fails visibly instead of leaking quietly.
- The only request it makes is for `jobs.json`, from the same folder, and only when served locally.
- Clicking a role's URL opens that site in a new tab, with no referrer sent. That is the only time the network is involved, and only because you clicked.

## Usage

Open the HTML file in a Chromium browser and choose `jobs.json` when prompted. `⌘S` / `Ctrl+S` saves back to it.

Optional: serve the folder to load `jobs.json` automatically, reachable from this computer only:

    python3 -m http.server 8000 --bind 127.0.0.1

then open `http://127.0.0.1:8000/job-tracker.html`. Without `--bind 127.0.0.1`, the server is reachable by anyone on the same network, such as university Wi-Fi.

## Data format

    {
      "version": 2,
      "categories": [ { "id", "name" } ],
      "orgs": [
        { "id", "categoryId", "name",
          "roles": [ { "id", "title", "status", "applied", "contact", "link", "location", "notes" } ] }
      ]
    }
