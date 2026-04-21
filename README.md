# Data-Enabled Science Seminar

GitHub Pages site for the **Data-Enabled Science Seminar** at the Department of
Mathematics, University of Houston — hosted jointly with the Networks Seminar.

## Editing the schedule

Every semester lives in its own small file under **`_data/semesters/`**. You
only ever need to touch two places:

- **`_data/semesters/<key>.yml`** — the talks for that semester.
- **`_data/seminars.yml`** — a one-page index with the current semester and the
  display order.

No templates or CSS need to be touched.

### Add a new talk to the current semester

Open `_data/semesters/<current>.yml` (for example `spring2026.yml`) and append
a new entry under `talks:`:

```yaml
- date: May 15 2026
  time: 12:00PM – 1:00PM
  note: Networks Seminar          # optional; leave out if not applicable
  speaker: Jane Doe
  affiliation: Department of X, University of Y
  title: Title of the talk
  abstract: |-
    Full abstract goes here. Markdown works:

    - Paragraph breaks are just blank lines.
    - **Bold**, *italic*, and [links](https://example.org) are supported.
    - Inline HTML is also allowed if you need it.
```

Fields:

| Field         | Required | Notes                                                           |
|---------------|----------|-----------------------------------------------------------------|
| `date`        | yes      | Free-form, e.g. `Jan 16 2026`                                   |
| `time`        | no       | Use en-dash form, e.g. `12:00PM – 1:00PM`                       |
| `note`        | no       | `Networks Seminar`, `virtual`, `PGH 646A`, etc. → colored badge |
| `speaker`     | no       | Omit or leave blank for TBD                                     |
| `affiliation` | no       | Rendered next to speaker name                                   |
| `title`       | no       | Shows `TBD` if omitted                                          |
| `abstract`    | no       | Markdown (or HTML); collapsible on the page                     |
| `holiday`     | no       | If set, renders a holiday card (e.g. `holiday: Thanksgiving`)   |

Badge colors are picked automatically from `note`: `Networks Seminar` is
indigo, `virtual` is green, anything else is gray.

### Start a new semester

1. Create a new file `_data/semesters/fall2026.yml` (or similar short key):

   ```yaml
   name: Fall 2026
   talks:
     - date: Aug 28 2026
       # ...
   ```

2. In `_data/seminars.yml`, add the new key to the top of `order:` and set it
   as `current:`:

   ```yaml
   current: fall2026
   order:
     - fall2026        # ← new semester at the top
     - spring2026
     - fall2025
     # ... rest unchanged
   ```

The previous semester automatically moves into the **Past Semesters** archive
with a bracketed talk count. Past semesters appear in the order you list them
in `order:`.

### Removing a semester

Delete its file from `_data/semesters/` and remove its key from `order:` in
`_data/seminars.yml`. The page will silently skip any key in `order` whose
file is missing, so partial edits are safe.

### Change site-level settings

`_config.yml` holds the site title, description, organizer contact, and meeting
time/location that populate the header and footer.

### Tweak styles

Edit `assets/css/style.css`. All UH-brand colors are at the top of the file as
CSS variables (`--uh-scarlet`, etc.).

## Local preview

Requires **Ruby ≥ 2.7** (the current `github-pages` gem no longer supports
older Rubies; macOS system Ruby 2.6 won't work — install a newer Ruby via
`rbenv`, `asdf`, or Homebrew first).

```bash
bundle install
bundle exec jekyll serve
```

The site then builds at <http://127.0.0.1:4000>. Edits to any data file or
`index.html` are picked up automatically; edits to `_config.yml` require a
server restart.

If local previews are inconvenient, pushing to a branch on GitHub and
inspecting the Pages build is also a fine workflow — builds take ~1 minute.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. In the repo's **Settings → Pages**, set *Build and deployment* to
   *Deploy from a branch*, branch `main` (root).
3. GitHub builds and serves the site at
   `https://<user>.github.io/<repo>/` within ~1 minute.

## File layout

```
.
├── _config.yml                         # site metadata (title, organizer, meeting info)
├── _data/
│   ├── seminars.yml                    # ← current semester + display order
│   └── semesters/
│       ├── spring2026.yml              # ← one file per semester (edit these to add talks)
│       ├── fall2025.yml
│       └── …
├── _includes/talk.html                 # template for a single talk card
├── assets/css/style.css                # UH-scarlet theming
├── index.html                          # page template (Liquid + HTML)
├── Gemfile                             # Jekyll/GitHub-Pages gem stack for local previews
├── .gitignore                          # ignores _site/, .jekyll-cache/, Gemfile.lock, …
└── README.md
```
