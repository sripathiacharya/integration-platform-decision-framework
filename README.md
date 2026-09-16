# Right Tech, Right Reason — Integration Platform Framework

Source for the integration platform decision framework (SAP CI vs MuleSoft),
published via GitHub Pages.

## Structure

- `index.md` — Problem statement + principles (edit this for wording/framing changes)
- `reference.md` — Full decision map (Mermaid diagram) + reference tables + capability registry
- `decision-tool.html` — The interactive click-through decision wizard (raw HTML/JS — not markdown, since it needs to run in the browser)
- `_config.yml` — Jekyll config (theme, markdown settings)

## Enabling GitHub Pages

1. Push this content to your repo's `main` branch (root, or a `/docs` folder — adjust Pages settings to match).
2. In the repo: **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Branch: `main`, folder: `/ (root)` (or `/docs` if you used that).
5. Save. Your site will be live at `https://<your-org-or-username>.github.io/<repo-name>/` within a minute or two.

## Editing day to day

- **Changing the problem statement or principles** → edit `index.md` directly on GitHub (or locally + PR). It's plain markdown — no HTML to navigate.
- **Adding a capability to the registry, or changing the decision map** → edit `reference.md`. The Mermaid diagram is a fenced code block-equivalent raw HTML `<pre class="mermaid">` block — edit the node text/arrows directly.
- **Changing the wizard's questions or logic** → edit `decision-tool.html`. This one does need HTML/JS familiarity, or ask Claude to update it and paste the result back in.

## Why this split

- Markdown pages (`index.md`, `reference.md`) render through Jekyll into styled HTML automatically — easy for anyone to edit via git, reviewable via pull request, versioned.
- The wizard is excluded from Jekyll processing (see `include:` in `_config.yml`) and served exactly as written, since it needs to execute JavaScript in the browser, which markdown can't do.
