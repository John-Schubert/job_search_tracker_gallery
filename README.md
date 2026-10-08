# Job Search Tracker — Screenshot Gallery

A public, static timeline of screenshots from a self-hosted job search
tracker. Every screenshot shows **fictional example data**: made-up companies,
contacts and notes from the project's demo mode. No real applications appear
here.

**Live gallery:** https://john-schubert.github.io/job_search_tracker_gallery/

**Source code (MIT):** https://github.com/John-Schubert/job_search_tracker

## What the project is

A small web app for keeping a job search organised, served on a home network
from a Raspberry Pi so a laptop and a phone see the same list.

- **Tracker:** one row per application, edited in place and saved as you
  type. Sort, search, filter by status. Follow-ups due soon are shaded amber
  and overdue ones red. Every change is recorded, and deleted rows can be
  restored.
- **Log:** dated free-text notes, each linked to nothing, to a company, or to
  one specific application. The tracker's own events (status changes, rows
  added or removed) appear in the same timeline.

It is one Python file using only the standard library, with SQLite for
storage and two plain HTML pages. There is no login, so the server only
answers clients on private network addresses and rejects the kinds of request
a hostile website could send through a browser.

## How it was built

Built with Claude Code. The first version was a single HTML page that kept its
data in the browser; the project moved the data to a server so several devices
could share it, then added the change history, the log, and the network
safeguards. The code repository's README has the design notes and the API.

## Adding a new snapshot

Start the demo, which serves fictional data on its own port:

```bash
python3 ~/job_tracker/examples/demo.py
```

Capture the pages from `http://localhost:8767/` (never from the live
tracker), save one PNG per view key in `manifest.json` to the source folder,
then run:

```bash
scripts/add_snapshot.sh "optional note about what changed"
```

This copies the PNGs into a new dated folder under `snapshots/` and appends
an entry to `manifest.json`. It does not commit or push.
