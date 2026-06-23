# Deployment Instructions - orient (assistant.lease)

This site is a static three-file bundle for the orient marketing site, served at the apex `assistant.lease`. The recommended path is **GitHub Pages with a custom domain**, keeping deployment entirely inside GitHub. Do not wire this through Vercel.

---

## 0. Prerequisites

- A GitHub account with push access to the `TechDaddyFairy` (or chosen) org.
- DNS access for the `assistant.lease` apex domain (currently 308-redirects to `www.oceanmachine.ai` via Vercel - that redirect must be removed first, see Step 5).
- Local git configured with the correct identity:

  ```bash
  git config user.name  "Ian McDonald"
  git config user.email "imc@icsmultimedia.com.au"
  ```

---

## 1. Create the GitHub repository

```bash
cd /home/user/workspace/assistant-lease-site
git init
git config user.name  "Ian McDonald"
git config user.email "imc@icsmultimedia.com.au"
git add .
git commit -m "Initial commit - orient marketing site"
git branch -M main
```

Create the remote (one of):

- Web: https://github.com/new - owner `TechDaddyFairy`, name `assistant-lease-site`, **Public**, no README/license/gitignore (we already have a README).
- CLI: `gh repo create TechDaddyFairy/assistant-lease-site --public --source=. --remote=origin --push`

If created via the web UI:

```bash
git remote add origin git@github.com:TechDaddyFairy/assistant-lease-site.git
git push -u origin main
```

---

## 2. Enable GitHub Pages

On the repository page:

1. **Settings** → **Pages**.
2. **Source**: `Deploy from a branch`.
3. **Branch**: `main` / `/ (root)`.
4. Save.

GitHub will build and publish to `https://techdaddyfairy.github.io/assistant-lease-site/` within ~60 seconds. Confirm the page renders correctly before attaching the custom domain.

---

## 3. Attach the custom domain inside GitHub

Still on **Settings** → **Pages**:

1. Under **Custom domain**, enter `assistant.lease` and save.
2. GitHub creates a `CNAME` file on `main` containing `assistant.lease`.
3. Tick **Enforce HTTPS** once the cert provisions (usually 5 to 15 minutes after DNS resolves).

---

## 4. Remove the old Vercel redirect

The apex `assistant.lease` currently 308-redirects to `www.oceanmachine.ai` via a Vercel project. Before DNS will resolve to GitHub Pages, that redirect must be removed.

In Vercel (manual, web UI only):

1. Open the project that owns the `assistant.lease` domain.
2. **Settings** → **Domains** → remove `assistant.lease` from that project.
3. Do not add it to any other Vercel project.

This is the only Vercel touch required. Everything else lives in GitHub.

---

## 5. DNS configuration

Set the apex `assistant.lease` to point at GitHub Pages.

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | 3600 |
| A | @ | 185.199.109.153 | 3600 |
| A | @ | 185.199.110.153 | 3600 |
| A | @ | 185.199.111.153 | 3600 |
| AAAA | @ | 2606:50c0:8000::153 | 3600 |
| AAAA | @ | 2606:50c0:8001::153 | 3600 |
| AAAA | @ | 2606:50c0:8002::153 | 3600 |
| AAAA | @ | 2606:50c0:8003::153 | 3600 |
| CNAME | www | techdaddyfairy.github.io. | 3600 |

(Replace `techdaddyfairy.github.io.` with the actual Pages host if the org is different.)

Verify:

```bash
dig +short assistant.lease
dig +short www.assistant.lease
curl -I https://assistant.lease
```

You should see GitHub's `185.199.x.x` block and a `200 OK` from `https://assistant.lease`.

---

## 6. Smoke checks after going live

Open `https://assistant.lease` and confirm:

- Hero loads with Instrument Serif heading "The pricing assistant for the leasing team."
- Catchment SVG diagram renders with a pulsing subject dot.
- Dark-mode toggle in the header flips colours and persists across reload.
- Mobile layout collapses cleanly at 760px and 640px breakpoints.
- All `mailto:` links point at `imc@oceanmachine.ai`.
- No console errors.
- Pagespeed / Lighthouse: aim for 95+ on Performance, Accessibility, Best Practices, SEO.

---

## 7. Subsequent updates

To ship a change:

```bash
cd /home/user/workspace/assistant-lease-site
# edit files...
git add .
git commit -m "Describe the change"
git push
```

GitHub Pages rebuilds within 30 to 90 seconds. No further action needed.

---

## 8. Rollback

```bash
git revert HEAD
git push
```

Or check out a known-good commit:

```bash
git checkout <sha> -- index.html styles.css favicon.svg
git commit -m "Roll back to <sha>"
git push
```

---

## Owner

Ian McDonald, Ocean Machine - [imc@oceanmachine.ai](mailto:imc@oceanmachine.ai)
