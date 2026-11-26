# JEREMY_HANDOFF.md — Mika Amir (Mikamir) websites

Handoff from Claude to Jeremy. Scope: **all websites built for Mika Amir-Anzwieg (artist name: Mikamir)**, Shaked Miller's guitarist.
Everything below was checked against the live sites, the git repos and GitHub settings on 2026-11-26. Where something could not be checked, it says so.

Client = **Shaked Miller** (she/her). Subject of the sites = **Mika Amir-Anzwieg**.

---

## 0. TL;DR

| What | Live URL | Source |
|---|---|---|
| Musician site: Portfolio + CV (main) | https://mikamirportfolio.github.io/ (CV view: `/#cv`) | GitHub `MIKAMIRPORTFOLIO/mikamirportfolio.github.io`, branch `main`, `/index.html` |
| Videographer site | https://mikamirportfolio.github.io/videographer/ | same repo, `/videographer/index.html` |
| Old duplicate (stale, not updated since 2026-11-19) | https://shakednmika-bot.github.io/mikamirportfolio/ | GitHub `shakednmika-bot/mikamirportfolio`, branch `main` |
| Claude-hosted copy of the musician site (stale-ish) | https://claude.ai/artifact/Mg3EPQaEnvqLeG3wDH5mVq | claude.ai artifact, slug `a76a27ae-9ee6-4d00-873f-21793c80d958` |
| CV document (editable doc) | https://claude.ai/artifact/19oueJi7o5wKfzA8AG6vTQ | Claude Docs, doc id `013adba7-44b8-4048-bf13-3f1252279f07` |
| Portfolio document (editable doc, with embedded videos) | https://claude.ai/artifact/XakgrzwJL8MkPQTUBSEFo8 | Claude Docs, doc id `f7a8a0a0-9971-4fad-8845-6074ef06fe03` |

**The source of truth is the GitHub repo `MIKAMIRPORTFOLIO/mikamirportfolio.github.io`.** Edit there; everything else is secondary.

Not in scope / not touched in this session: shakedmillercv.github.io, shakedmiller.com, Shaked's Bandzoogle store. I did not build or edit them, so I have no verified facts about them.

---

## 1. Site inventory

### 1.1 Main site — mikamirportfolio.github.io

- **Live:** https://mikamirportfolio.github.io/ — Portfolio view by default; CV view at `https://mikamirportfolio.github.io/#cv`
- **Repo:** https://github.com/MIKAMIRPORTFOLIO/mikamirportfolio.github.io (public)
  - Owner account: **MIKAMIRPORTFOLIO** (GitHub shows the login in caps; URLs are case-insensitive). This is a GitHub account Shaked created on 2026-11-19 only so the address could be `mikamirportfolio.github.io`.
  - Branch: `main` (only branch). Default branch: `main`.
  - Collaborator with write access: **shakedyyy0-jpg** (invited and accepted 2026-11-19). This is the account Claude pushes with. GitHub Pages shows "Last deployed by shakedyyy0-jpg".
  - Claude GitHub App: installed on MIKAMIRPORTFOLIO by Shaked.
  - Local clone (Claude's workspace): `/home/claude/mikamirportfolio.github.io`
- **Hosting:** GitHub Pages, "Deploy from a branch" → `main` / `(root)`. It's a *user site* repo (name = `<account>.github.io`), so it serves at the domain root.
  - `.nojekyll` is present → files are served as-is, no Jekyll build.
  - HTTPS enforced (GitHub default domain).
  - **Deploy = `git push` to `main`.** The Pages build takes ~30–60 s; a brand-new path can 404 for about a minute.
- **Domain:** none. No custom domain, no CNAME file, no DNS. Shaked decided **not to pay for a domain** (asked for mikamirportfolio.com; it looked unregistered on 2026-11-19 via the Verisign RDAP lookup, but she declined to buy).
- **Stack:** plain static HTML/CSS/vanilla JS. No build step, no framework, no package.json.
  - Fonts: Google Fonts (Bodoni Moda, Karla, DM Mono) loaded from fonts.googleapis.com.
  - Two "pages" in one file, switched by URL hash: `#cv` shows the CV, anything else shows the Portfolio. Router is a ~15-line inline `<script>` at the end of `index.html` (`show()` toggles `#view-portfolio` / `#view-cv`).
  - Print CSS: `@page A4, margin 0`, `print-color-adjust: exact` keeps the dark background in PDFs.
  - Open Graph / WhatsApp preview: `og:image` = `https://mikamirportfolio.github.io/og.jpg?v=2` (1200×630, "MIKA AMIR" card).
- **Files (repo root):**

```
.nojekyll                      # disables Jekyll
README.md                      # 1 line, from GitHub's "Add README"
index.html                     # Portfolio + CV (hash-routed)
og.jpg                         # 1200x630 link-preview card
live_guitar.jpg                # hero photo of Mika (screen-captured from her Instagram, ~450x600 – low-res)
melting_ice_queen.jpg          # album art (screen-captured from Instagram, ~600x600)
stage_light.jpg                # Mika on stage (screen-captured from Instagram)
press1.jpg press2.jpg          # press shots Mika shot (sent by Shaked on WhatsApp, resized to 1600px)
wed_*.jpg (5)                  # wedding photos Mika shot in Berlin (WhatsApp, resized to 1600px)
*_live.mp4 + *_poster.jpg      # embedded videos and their still frames:
  shaked_live.mp4              #   Mika with Shaked Miller's trio
  hachalutz_live.mp4           #   Mikamir & band, HaChalutz, Be'er Sheva, 13 Mar 2026
  mikamir_live_sax.mp4         #   Mikamir guitar/vocals/sax
  mikamir_live_band.mp4        #   Mikamir & band with violin (venue unknown)
  nada_live.mp4                #   Nada at Little Stage Club (Mika filmed it)
  kodesh_live.mp4              #   Edog & Shablul "Kodesh" Live Session (Mika filmed & edited)
videographer/                  # the videographer site, see 1.2
JEREMY_HANDOFF.md              # this file
```

  All `.mp4` files in the root came from Shaked via WhatsApp and are uploaded unchanged. Posters are single frames grabbed with ffmpeg, chosen so there is no burned-in text on them (Shaked asked: **no text on images**).

### 1.2 Videographer site — mikamirportfolio.github.io/videographer/

- **Live:** https://mikamirportfolio.github.io/videographer/
- **Repo / hosting / deploy:** same repo and Pages setup as 1.1; source is `videographer/index.html`.
- **Stack:** plain static HTML/CSS, no JS. Fonts: Anton, Karla, DM Mono (Google Fonts).
- **Own OG card:** `videographer/og.jpg` ("MIKA AMIR – Videographer & Video Editor", bass player frame from her jazz-session video).
- **Shares assets with the main site via `../`:** `../kodesh_live.mp4`, `../nada_live.mp4`, their posters, `../press1.jpg`, `../press2.jpg`, `../wed_*.jpg`. Don't delete those from the root.
- **Files in `videographer/`:**

```
index.html
og.jpg
raufman_live.mp4         + _poster.jpg   # Tal Raufman live (IG @raufman_)
daniel_rubin_live.mp4    + _poster.jpg   # Daniel Rubin live
ariela_baruch_1.mp4      + _poster.jpg   # Ariela Baruch live, social edit with subtitles
ariela_baruch_2.mp4      + _poster.jpg   # Ariela Baruch live, social edit (poster is the top 60% of a frame to avoid subtitles)
jazz_session.mp4         + _poster.jpg   # live session: double bass, drums, sax (artist name unknown)
rooftop_live.mp4         + _poster.jpg   # Sofar Sounds rooftop show (artist/city unknown)
```

  These were re-encoded from Shaked's uploads (originals 25–200 MB, iPhone HEVC .mov/.MP4) to H.264 720p so the repo stays small and they stream fast:

```bash
ffmpeg -i INPUT -c:v libx264 -preset veryfast -crf 27 \
  -vf "scale='if(gt(iw,ih),-2,720)':'if(gt(iw,ih),720,-2)',fps=30" \
  -c:a aac -b:a 128k -movflags +faststart OUTPUT.mp4
```

### 1.3 Old duplicate — shakednmika-bot.github.io/mikamirportfolio

- **Live (still up):** https://shakednmika-bot.github.io/mikamirportfolio/ — the first GitHub version (2026-11-19). It does **not** have later fixes (Be'er Sheva, credit order, new OG card, videographer site).
- **Repo:** https://github.com/shakednmika-bot/mikamirportfolio, branch `main`, Pages from `main` / root. Collaborator shakedyyy0-jpg. Local clone: `/home/claude/mikamirportfolio`.
- **Status:** obsolete. I asked Shaked whether to delete it; no answer yet. See §5.

### 1.4 Claude artifact copy — claude.ai/artifact/Mg3EPQaEnvqLeG3wDH5mVq

- The page was first built here, then moved to GitHub. Public (shared by Shaked), title "Mikamir", version `1795120375-bc24`.
- Has the same Portfolio + CV content as of 2026-11-19 evening (includes Be'er Sheva), but **no videographer section** and the older OG text. The link is not the one she sends anymore.
- Republish with the Claude artifacts tool `publish_files` (slug above, `mode: patch`, `shared_live: "public"`, `artifact_title: "Mikamir"`).

### 1.5 Claude Docs (editable documents)

- **CV doc** — "Mika Amir-Anzwieg – Artist CV": https://claude.ai/artifact/19oueJi7o5wKfzA8AG6vTQ (doc `013adba7-44b8-4048-bf13-3f1252279f07`, body node `c5c2c44c-b634`).
- **Portfolio doc** — still titled "Mika Amir-Anzwieg – Guitar Portfolio": https://claude.ai/artifact/XakgrzwJL8MkPQTUBSEFo8 (doc `f7a8a0a0-9971-4fad-8845-6074ef06fe03`, body node `6275b315-bcb4`). Contains uploaded photos and videos.
- These were the first deliverables; the website supersedes them. Keep them in sync only if Shaked asks. Shaked herself trimmed the end of the portfolio doc's "About" paragraph — leave that as she left it.

---

## 2. How it was built (chronological, with decisions)

1. **Research (2026-11-19).** Mika's Instagram is **@mikamir_** (Shaked first gave @mikamir — a different, private account). Sources used: her Instagram bio + posts + tagged posts + highlights ("Touring", "Live"), her Carrd site `mikamir.carrd.co`, Spotify artist `4HkeAp8Q2Gbpuzt1CCIo2b`, YouTube `@Mikamirmusic`. Web search returned nothing about her.
2. **Fact rules.** Only facts Shaked gave or that appear on a public page. Unverified items were marked and asked about. Shaked then supplied: Shaked Miller trio since 2025; PORT NOO Germany tour 2026 on guitar (Hamburg Reeperbahn, Munich, Bremen, Kiel, Berlin, Blankenburg, Nordendorf; TV: Bayerisches Fernsehen Abendschau; radio: radioeins); Georgia Cavallo (hired musician, 2027 tours); Lauren Lakis (EU tour April 2027); Berlin freelance gigs; Israel credits (Lea Haggai, MILLY/Lee Shai, Yam Gronich, Meirav Hellinger, Ori Kastiel, Avri G on bass, Aner Shapira tribute, two Mac Miller tributes); solo shows (Hall of Fame festival at Park HaYarkon Oct 2024, Tamuz Oct 2024, HaMertz 2 Dec 2024 incl. opening for Jonathan Lobel, HaChalutz Be'er Sheva 13 Mar 2026); EP *Push Sadness Away* Jan 2027; self-taught on guitar/bass/sax/drums/keys; languages Hebrew + English; phone +49 176 41120684; videography credits (Liam Hakmon, Daniel Rubin & Nunu at Barby, Nastia Rod, Peled, Ariela Baruch, Roni Kaspi/Roni Poni, Gali Yolus, Edog & Shablul "Kodesh", Lara Snow BTS, Nada).
3. **Claude Docs first** (CV + portfolio docs), then Shaked asked for "beautiful, in Mika's style" → **hand-built HTML page** (dark "stage" palette: black, violet `#b98aff`, amber `#e7a75e`; Bodoni Moda display font), because Docs can't style or play several videos nicely.
4. **Videos:** Instagram/YouTube can't be embedded as playable files (Instagram streams via MSE, no downloadable file), so Shaked sent the files over WhatsApp and they're hosted as `.mp4` next to the page. Every embedded video also has a clickable online link.
5. **Redesign** on Shaked's feedback: numbered sections, no text over images, posters picked without burned-in subtitles.
6. **PDF:** print CSS added so exported PDFs keep the dark background. PDFs were generated with headless Chrome (§4.5).
7. **Two views in one site:** Portfolio and CV, hash-routed.
8. **Moving off claude.ai:** a claude.ai link can't have a custom name or a custom WhatsApp preview image, so → GitHub Pages.
   - First repo under **shakednmika-bot** (the account signed in in the app's browser pane). Claude's GitHub identity is **shakedyyy0-jpg**, so `add_repo` refused push until shakedyyy0-jpg was invited as a collaborator and Shaked accepted it. Pushed, enabled Pages → `shakednmika-bot.github.io/mikamirportfolio`.
   - Shaked wanted exactly `mikamirportfolio.com` → domain costs money → she declined → free alternative `mikamirportfolio.github.io` needs an account named `mikamirportfolio`. Shaked created account **MIKAMIRPORTFOLIO**; Claude created repo `mikamirportfolio.github.io` (with README so `main` exists), invited shakedyyy0-jpg, Shaked accepted and installed the Claude app, then pushed. User-site repos publish from `main` automatically.
9. **OG card** rebuilt in the style of Shaked's own site card (big condensed name left, photo right), rendered from a small HTML file with headless Chrome using the local font **Anton**.
10. **Facts fixed after review:** credit order (newest first), HaChalutz = Be'er Sheva (Shaked confirmed), Shaked Miller YouTube link switched to the public video `u5vH609oWXU` (the first link `_1hQoks6Ajg` was private).
11. **Videographer site (2026-11-22)** at `/videographer/` in the same repo (no new account/permissions needed). 7 videos from Shaked + the Kodesh session.

### Problems hit and fixes

| Problem | Fix |
|---|---|
| Wrong Instagram handle (@mikamir private) | Shaked corrected to @mikamir_ |
| Built-in browser not signed in to Instagram → private content invisible | Shaked signed in; public account anyway |
| Instagram/YouTube videos can't be embedded as files | Shaked sends files; host .mp4; always add the online link too |
| Instagram images can't be downloaded from the shell (network allowlist) | Displayed each image full-viewport in the browser pane and screenshotted it (≈450–600 px, low-res) — replace with originals when possible |
| "מהמרץ" misread as "March" | It means **HaMertz 2** (venue). Corrected everywhere |
| Docs rename via API didn't change visible title | Title must be renamed by hand on claude.ai |
| claude.ai link: no custom name/preview | Moved to GitHub Pages |
| `gh api` can't create repos/read settings through the session proxy | Create repos and change settings in the browser pane (signed in as the owner account); push via git |
| `add_repo` "need push access" | Invite shakedyyy0-jpg as collaborator + Shaked accepts + Claude GitHub App installed on the owner account |
| I once copied a `.git` folder over a clone (`cp -r site/. .`) | Re-cloned and moved the correct `.git` back. Use `rsync --exclude .git` or `tar --exclude=.git` |
| New Pages path 404s right after push | Wait ~60 s, reload with `?v=N` |
| WhatsApp keeps old previews | Bump the query string on `og:image` (`og.jpg?v=3`), new chats pick it up |
| `sed` with `&` in replacement broke text ("CVamp;") | Use Python `str.replace` for HTML edits |

---

## 3. Access

No passwords or tokens are written here. Nothing secret is stored in the repo.

| Access | Where it lives / how to get it |
|---|---|
| **GitHub account MIKAMIRPORTFOLIO** (repo owner) | Shaked's login. Signed in inside the Claude desktop app's **built-in browser pane** (as of 2026-11-26). Settings pages ask for "sudo mode" (email verification to the account's email) → only Shaked can complete that. |
| **GitHub account shakedyyy0-jpg** | The GitHub account connected to Shaked's claude.ai (Settings → Connectors → GitHub). Claude sessions push with it through the session git proxy. Write collaborator on both repos. |
| **GitHub account shakednmika-bot** | Shaked's other account; owns the old duplicate repo. |
| **Claude GitHub App** | Installed by Shaked on MIKAMIRPORTFOLIO and on shakednmika-bot. |
| Session repo attach | In a new Claude session: `add_repo` with `owner: "MIKAMIRPORTFOLIO"`, `repo: "mikamirportfolio.github.io"`, `access: "push"`, then clone (see §4.1). |
| SSH keys / PATs | None used. Don't create any. |
| Domain / DNS | None. |
| claude.ai artifacts + Docs | Owned by Shaked's claude.ai account; editable from any Claude session on that account (artifacts tools / Claude Docs tools). |
| Built-in browser site approvals | github.com, open.spotify.com, youtube.com, mikamir.carrd.co, shakednmika-bot.github.io allowed "site"-wide. Instagram is reachable; Shaked is signed in there as **shakedmiller**. |

**What Shaked must approve/grant so Jeremy has full edit access:**
1. If Jeremy runs as a Claude session on Shaked's claude.ai account: nothing new — `add_repo` (push) works because shakedyyy0-jpg is already a collaborator.
2. If Jeremy uses a **different GitHub identity**: Shaked (signed in as MIKAMIRPORTFOLIO) invites that account at `https://github.com/MIKAMIRPORTFOLIO/mikamirportfolio.github.io/settings/access` with **Write** (or Maintain/Admin for settings), and the invite is accepted from that account. Install the Claude GitHub App for that repo if needed: `https://github.com/apps/claude`.
3. For **repo settings** (Pages, collaborators, custom domain, deleting repos): needs the owner account signed in (MIKAMIRPORTFOLIO) + email "sudo" confirmation by Shaked.
4. For a **custom domain**: Shaked must buy it and pay (she declined so far), then give DNS access at the registrar.

---

## 4. Working guide

### 4.1 Get the code

```bash
# in a Claude session: first add_repo(owner="MIKAMIRPORTFOLIO", repo="mikamirportfolio.github.io", access="push")
git clone --depth 1 https://github.com/MIKAMIRPORTFOLIO/mikamirportfolio.github.io /home/claude/mikamirportfolio.github.io
cd /home/claude/mikamirportfolio.github.io
git log --oneline -5
```

### 4.2 Edit

- Text/layout: edit `index.html` (Portfolio = `#view-portfolio`, CV = `#view-cv`) or `videographer/index.html`.
- Design tokens are at the top of each `<style>` in `:root` (colors, fonts). Keep: dark only, no text over images/video, captions under media, every video has an online link.
- For HTML edits prefer Python string replacement over `sed`:

```bash
python3 - <<'EOF'
p='index.html'; s=open(p).read()
old='<span>Live with band at HaChalutz, Be&#39;er Sheva</span>'
new='<span>…new text…</span>'
assert old in s; s=s.replace(old,new,1); open(p,'w').write(s)
EOF
```

- Add a video:

```bash
ffmpeg -i /path/in.mov -c:v libx264 -preset veryfast -crf 27 \
  -vf "scale='if(gt(iw,ih),-2,720)':'if(gt(iw,ih),720,-2)',fps=30" \
  -c:a aac -b:a 128k -movflags +faststart videographer/new_clip.mp4
# poster: pick a frame without on-screen text; check a contact sheet first
ffmpeg -i videographer/new_clip.mp4 -vf "fps=1,scale=90:-2,tile=20x2" -frames:v 1 /tmp/sheet.jpg
ffmpeg -ss 12 -i videographer/new_clip.mp4 -frames:v 1 -q:v 3 videographer/new_clip_poster.jpg
```

  Then add a `<video controls playsinline preload="metadata" poster="…" src="…">` block + caption + online link. Keep files < 25 MB (GitHub hard limit is 100 MB per file).

### 4.3 Check locally

```bash
cd /home/claude/mikamirportfolio.github.io
google-chrome --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --window-size=1280,4200 --virtual-time-budget=4000 \
  --screenshot=/tmp/shot.png "file://$PWD/index.html"            # Portfolio
google-chrome --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --window-size=1280,2600 --virtual-time-budget=3000 \
  --screenshot=/tmp/cv.png "file://$PWD/index.html#cv"           # CV
google-chrome --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --window-size=1280,4200 --virtual-time-budget=4000 \
  --screenshot=/tmp/vg.png "file://$PWD/videographer/index.html" # Videographer
```

Look at the screenshot once, fix, then push.

### 4.4 Deploy

```bash
git add -A
git -c user.name="Mikamir" -c user.email="mikamir.music@gmail.com" commit -m "Describe the change"
git -c push.negotiate=true push origin main
```

Wait ~60 s, then verify in the browser pane: open `https://mikamirportfolio.github.io/?v=N` and check title, that all `<video>`s have `readyState>0` and images load:

```js
[document.title, [...document.querySelectorAll('video')].filter(v=>v.readyState>0).length+'/'+document.querySelectorAll('video').length,
 [...document.images].filter(i=>i.naturalWidth>0).length+'/'+document.images.length]
```

If the change touched the link preview, bump `og.jpg?v=N` in the `og:image` meta.

### 4.5 PDFs

```bash
# whole site (Portfolio + CV) in one PDF
python3 - <<'EOF'
s=open('index.html').read()
s=s.replace('<div class="view" id="view-cv" hidden>','<div class="view" id="view-cv" style="break-before:page">')
s=s.replace("window.addEventListener('hashchange', show);\n  show();",'')
open('/tmp/_all.html','w').write(s)
EOF
cp *.jpg /tmp/ && google-chrome --headless=new --no-sandbox --disable-gpu --no-pdf-header-footer \
  --virtual-time-budget=8000 --print-to-pdf="/tmp/Mika Amir - Portfolio & CV.pdf" file:///tmp/_all.html
```

Deliver PDFs with `SendUserFile`. Videos show as still frames in PDFs.

### 4.6 Rollback

```bash
git log --oneline -10
git revert <bad_commit_sha>            # creates an undo commit; preferred
git -c push.negotiate=true push origin main
# or roll a single file back:
git checkout <good_sha> -- index.html && git commit -m "Restore index.html" && git push origin main
```

Never force-push to `main`.

### 4.7 New site with the same method

- **New page under the same domain (no new permissions):** create a folder, e.g. `/press/index.html`, reuse root assets via `../`, push → live at `https://mikamirportfolio.github.io/press/`.
- **New site at its own `<name>.github.io`:**
  1. Shaked creates a GitHub account named `<name>` (Claude may not create accounts) and signs in to it in the app's browser pane.
  2. In the browser pane: `https://github.com/new` → name `<name>.github.io`, Public, **Add README = On** → Create.
  3. Repo → Settings → Collaborators → invite `shakedyyy0-jpg` (Write). Shaked accepts it while signed in as shakedyyy0-jpg: `https://github.com/<NAME>/<name>.github.io/invitations`.
  4. Shaked installs the Claude app on the new account: `https://github.com/apps/claude` → only that repo.
  5. `add_repo(owner="<NAME>", repo="<name>.github.io", access="push")`, clone (§4.1), add `index.html` + `.nojekyll` + assets, push (§4.4).
  6. User-site repos publish from `main` automatically; confirm at `…/settings/pages`.
  7. Add OG tags + a 1200×630 `og.jpg` (template: render a small HTML card with headless Chrome; Anton font is installed locally).
- **Custom domain** (only if Shaked pays): buy at a registrar; DNS: apex `A` records → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153 (+ `AAAA` 2606:50c0:8000::153 … 8003::153), `www` `CNAME` → `<account>.github.io`; add a `CNAME` file containing the domain; set it in Settings → Pages; enable HTTPS.

---

## 5. Open items

1. **Delete the old duplicate?** `shakednmika-bot.github.io/mikamirportfolio` is stale. Asked Shaked; no answer. Deleting a repo needs the shakednmika-bot owner + her OK.
2. **Unknown artist names** on the videographer site: the jazz session (double bass, drums, sax) and the Sofar Sounds rooftop show (also its city).
3. **Single name:** first single from *Push Sadness Away* (released ~2026-11-20) — Shaked didn't know the name; listed unnamed.
4. **Low-res images:** `live_guitar.jpg`, `melting_ice_queen.jpg`, `stage_light.jpg` are screenshots from Instagram. Replace with originals from Mika if she sends them.
5. **Photo credits:** Shaked said she'd add credits herself; none on the site yet.
6. **Dates:** Instagram posts suggest Hall of Fame and HaMertz 2 were in 2025; Shaked confirmed the site's **2024** dates. Keep 2024.
7. **Shaked's YouTube title typo:** the public video `u5vH609oWXU` is titled "Liver show" — suggested fixing in YouTube Studio (her action, not ours).
8. **Portfolio doc title** still "Guitar Portfolio" → must be renamed by hand on claude.ai (API rename didn't apply).
9. **Claude artifact copy** (`Mg3EPQaEnvqLeG3wDH5mVq`) lags the GitHub site (no videographer part, older OG text). Either republish from the repo's `index.html` or stop sharing it.
10. Unsure: video `mikamir_live_band.mp4` (with violin) — show/venue unknown; captioned without a place. `shaked_live.mp4` was assumed to be the Shaked Miller trio from the footage.

---

## 6. Working with Shaked

- **Never ask her to do something herself — do it.** The only exception: when a permission or access is needed (signing in, accepting an invite, installing an app, paying, "sudo" email confirmations, creating an account). Then give her the exact link and the one step.
- **Answers short and to the point.** She writes Hebrew; answer in Hebrew.
- Don't invent facts. If something isn't confirmed by her or a public page, leave it out or mark it, and ask in one short line.
- No text over photos/videos. Every embedded video also gets a clickable online link.
- Things she sends over WhatsApp (photos, videos) go straight into the sites; she said all of Mika's material may be used and she'll add credits herself.
- She doesn't want to pay for domains.
- Accounts: shakedyyy0-jpg (connected to Claude), shakednmika-bot, MIKAMIRPORTFOLIO. Mika's contact on the site: mikamir.music@gmail.com, +49 176 41120684, Instagram @mikamir_.
