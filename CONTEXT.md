# FDE Hub — Project Context

## What this is
A personal resource launchpad built as a single `dashboard.html` file. It is NOT a learning tracker — it is a bookmark/link hub for quick access to everything needed in the FDE (Forward Deployment Engineer) role at Salesforce.

## File location
`/Users/rwickramanayake/claude-projects/fde-learning/dashboard.html`

## Git repo
- Local git repo initialized at `/Users/rwickramanayake/claude-projects/fde-learning/`
- Remote: `https://github.com/rwickramanayake77/fde-hub.git`
- Push was pending at end of last session (needed GitHub Personal Access Token)

## Design
- Background: Salesforce dark navy `#032D60`
- All text white/near-white for visibility on dark background
- 7 category cards on the home screen, each with a colour accent

## Categories
| ID | Title | Colour |
|----|-------|--------|
| bootcamp | Bootcamp | #60A5FA (blue) |
| commercial | Commercial Team Enablement Videos | #A78BFA (purple) |
| architecture | Architecture | #F87171 (red) |
| agentscript | Agent Script | #A78BFA (purple) |
| datacloud | Data Cloud | #FB923C (orange) |
| dashboards | Key Dashboards | #34D399 (green) |
| customers | Customers | #F472B6 (pink) |

## Current resources (hardcoded in defaultResources array)
- **dashboards** → AI Spend (team24-portal.forge-prod.sfdcbt.net)
- **commercial** → ANZ Builder Onboarding — Dev Process: How We Work (Google Drive, Kane Lo, 2026/11/09)
- **customers / University of Melbourne** → Discovery Notes (Slack doc), Response to Agent Best Practice Questions (Google Doc)
- **customers / Christian Education Ministry** → FDE Overview (added via UI, stored in localStorage)
- **architecture / Discussion Threads** → SOMA for customer with 65 subagents (Slack thread)

## Key features
- **Edit mode** — yellow "Edit" button in topbar; pencil/trash icons on each item; inline edit form with title, desc, URL, group fields
- **Add item** — dashed "Add item" button appears in edit mode at the bottom of each section
- **Groups** — items can be grouped under a named section heading (e.g. "University of Melbourne", "Discussion Threads"); set via the Group field in the edit form
- **Pin / Favourites** — star icon on hover; pinned items appear in a "Pinned" row at the top of home
- **Recently Opened** — auto-tracked on click; last 6 shown in "Recently Opened" row at top of home; "Clear" button to wipe
- **Search** — always-visible search bar; searches title, description AND group name across all resources
- **localStorage persistence** — all edits (add/edit/delete items) save to localStorage key `fde_hub_v4`; pinned in `fde_pinned`; recent in `fde_recent`

## Data model
Each resource object:
```js
{
  id: "r1",           // unique string
  cat: "dashboards",  // matches a category id
  title: "AI Spend",
  desc: "Optional description",
  url: "https://...",
  group: "Optional group heading"  // omit if not grouped
}
```

## How to add new resources
Either:
1. Use Edit mode in the browser (pencil icon → fill form → Save). Saves to localStorage.
2. Add directly to the `defaultResources` array in `dashboard.html` and bump the localStorage version key (currently `fde_hub_v4` → change to `fde_hub_v5` in both `loadResources` and `saveResources` functions).

## Important implementation notes
- localStorage version is currently `fde_hub_v4` — bump to `v5` if you add new defaultResources and want to reset
- Items added via Edit UI are in localStorage only — not in the HTML file. To make them permanent, add them to `defaultResources` and bump the version.
- The `makeRitem` function renders each resource card; it auto-detects Slack URLs and shows the Slack icon
- Groups are rendered as section headings with a divider line; ungrouped items render first

## Pending
- Push to GitHub (`rwickramanayake77/fde-hub`) — needs GitHub Personal Access Token or GitHub MCP reconnect
- GitHub MCP was installed at end of session but required a restart to load tools
