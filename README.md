# Job tracker

Single-file HTML · Vanilla JS · No build, no dependencies

## Status

- App: done
- Storage: done

## Spec

- Data: everything lives in `jobs.json`; nothing is stored in the page or the browser
- Categories: up to 4 user-named tracks (e.g. Industry, PhD, Part-time)
- Structure: category → organisation → roles
- Role fields: role, contact, status, URL, location, notes
- Statuses: Not applied, Applied, Interview, Processing, Accepted, Rejected, Dropped
- Saving: `⌘S` / `Ctrl+S` writes back to the same file (File System Access API); falls back to import/export JSON in other browsers
- Migration: older `jobs.json` files are upgraded automatically on open

## Usage

Open the HTML file in a Chromium browser and choose `jobs.json` when prompted. `⌘S` / `Ctrl+S` saves back to it.

Optional: run `python3 -m http.server` in the folder to load `jobs.json` automatically.

## Data format

    {
      "version": 2,
      "categories": [ { "id", "name" } ],
      "orgs": [
        { "id", "categoryId", "name",
          "roles": [ { "id", "title", "status", "contact", "link", "location", "notes" } ] }
      ]
    }
