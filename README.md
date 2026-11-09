# Akij Takaful Life Insurance PLC — Website

A fast, bilingual (English / বাংলা) static website with an installable phone-app mode. No server or database needed — it runs on GitHub Pages or any web host.

## Put it online (GitHub Pages)
1. Create a repository on GitHub (Public).
2. Upload **everything in this folder** (keep `assets`, `icons` and `tools` as they are).
3. Settings → Pages → Source: *Deploy from a branch* → `main` / `(root)` → Save.
4. After 1–2 minutes the site is at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

To update: open a file on GitHub, click the pencil ✏️, edit, then **Commit changes**. The site updates in about a minute.

## Photos (board, management, staff, news, partners)
The site first looks for photos in `assets/img/…`, and if a photo is not there it loads it from the live website. To make the site fully independent of the live server, run this **once on a computer with Python 3** (no extra packages):

    python tools/download_photos.py

It downloads all 136 pictures into `assets/img/people`, `assets/img/news`, `assets/img/partners` and `assets/img/slides`. Then upload the new `assets/img` files to GitHub. Photos not yet downloaded keep loading from the live site.

## Folder map
| Path | What it is |
|---|---|
| `index.html` | Page structure (all pages live here, switched with `#plans`, `#claims`, …) |
| `assets/js/data.js` | **All content you will usually edit** |
| `assets/js/i18n-bn.js` | Bangla translations (`"English text":"বাংলা"`) |
| `assets/js/app.js` | Logic: pages, language switch, ATLI bot, quiz, animations (rarely edited) |
| `assets/css/style.css` | Design and animations |
| `assets/img/` | Logo, brand patterns, slider images, downloaded photos |
| `tools/` | Photo downloader |
| `manifest.webmanifest`, `sw.js`, `icons/` | Lets phones install the site as an app |

## Editing content (`assets/js/data.js`)
- **COMPANY** – the footer shows the credit rating (`rating`, currently A; add the rating agency in `ratingBy` if you like). The IDRA `licence` number can be added later; it appears only when filled in.
- **Plans** – `PLANS`: each plan has `id`, `u` (live product page number), `g` (goal: `save` `family` `child` `hajj` `retire`), `n` (name), `bn` (Bangla name), `tag`, `i` (intro), `f` (key facts `["Label","Value"]`) and `b` (benefits `["Title","Text"]`). To add one of the new plans, copy a whole `{...}` block, paste it after the last plan and change the text. Remove one of the "New plan — details coming" cards in `app.js` (`for(let i=9;i<=11;i++)`) when you add a real plan.
- **Branches** – `BR`: `["Division","Office name","Address","Manager","Designation","Phone"]`.
- **Staff** – `STAFF`: `["photo file name on the live server","Name","Role"]`. The About page and Staff list sort people into position levels automatically from the role text (CEO / DMD → Executive leadership; SEVP, SVP, VP, DVP, AVP, HoD, Consultant → Senior management; Manager → Management; Executive / Officer → Executives & officers; everyone else → Support teams).
- **Board of Directors** – `BD` in `app.js`; **Shariah Council** – `SH`.
- **Sales teams** – `TEAM` (retail, banca, group).
- **News** – `MEDIA`: `["id","date","title","summary"]`; full text in `STORIES["id"]`; photo path in `LIVE.media["id"]`. A story without full text shows its summary and a link to the live site.
- **Forms** – `FORMS`: `["download id","Form name","Category"]`.
- **Claims documents** – `CLAIMS`.
- **FAQ** – `FAQ`: `k` = keywords (also used by the ATLI bot), `q` question and `a` answer, each with `en` and `bn`.
- **Quiz** – `QUIZ`: question `q`, options `o`, correct option number `c` (0 = first), explanation `x`.
- **Policy terms** – `TERMS`.

## Bangla
Every English text is looked up in `assets/js/i18n-bn.js`. For new English text add a line: `"Your new text":"আপনার নতুন লেখা",`.

## Still to do before launch
- Add the 3 new retail plans (the site lists 8 of 11).
- Add the IDRA licence number to `COMPANY` when you want it shown.
- Confirm the source and period of "99% claims paid".
- Confirm the Karjahasana loan limit (plan pages say 85%, policy terms 1.15 say 90%).
- Add the full text of the 7 older news stories to `STORIES`.
- Official Bangla translation of the policy terms (English shown for now).
- Hospital and outlet search need a data feed from the live database.
- The ATLI bot answers from `FAQ` and fixed rules; it is not a live AI.
