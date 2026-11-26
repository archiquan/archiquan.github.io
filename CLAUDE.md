# archiquan.github.io: notes for Claude

Li (Archi) Quan's academic website. GitHub Pages publishes it from `main` (repo root), so
**a push to `main` is live in about a minute**. There is no build step: the whole site is one
static page, `index.html`.

## Layout

- `index.html`: every section (Home, Research, CV, Teaching, Contact)
- `papers/`: paper PDFs linked from Research
- `teaching/`: teaching evaluation PDF linked from Teaching
- `photo.jpg`, `robots.txt`, `sitemap.xml`, `google7940cca9b23662d8.html` (Search Console
  verification; leave it alone)
- `_config.yml`: keeps this note out of the published site

## PDF file names

The links in `index.html` point at these exact names (case-sensitive, hyphens, no spaces):

| Item | File |
|---|---|
| Job market paper, "Predictable Play with Simple Conjectures" | `papers/Predictable-Play-Simple-Conjectures.pdf` |
| "Choosing Your Competition: Predictable Subject Choice in China's Highest Exam" | `papers/Choosing-Your-Competition.pdf` |
| "Learning-Optimal Design of Data Markets" (with Yangbo Song) | `papers/Learning-Optimal-Data-Markets.pdf` |
| E100 teaching evaluation, Michaelmas 2025–26 | `teaching/E100-Teaching-Evaluation-2025-26.pdf` |

- **New draft of an existing paper:** copy it over the old file under the same name. Don't add a
  second file or change the link, so links people already have keep working.
- **New paper:** name it `papers/Short-Title-With-Hyphens.pdf` and give its entry the same
  `<div class="links"><a href="..." target="_blank" rel="noopener">PDF</a></div>` as the others.
- If it isn't clear which file is the newest draft, ask the user. Don't guess from file dates.

## Updating the site

1. Run `git pull` first, because the user sometimes uploads files on github.com.
2. Edit, then open `index.html` and check the changed section renders.
3. Publish only when the user has asked for the change to go on the site ("upload", "put on my
   website", "push"). Otherwise show the change and ask, because a push to `main` is public at once.
4. Commit as the user: `git config user.name "Archi Quan"`, `git config user.email "lq230@cam.ac.uk"`
   (repo-local).
5. After pushing, check the live site rather than assuming. Fetch with a cache-busting query
   (`?v=$RANDOM`) until the new text appears, and for a PDF compare the live file's `shasum -a 256`
   with the source file.

## Push access on a new Mac

Each machine gets its own deploy key, so one can be revoked without touching the other.

```bash
ssh-keygen -t ed25519 -N "" -C "archiquan.github.io deploy key (<machine name>)" -f ~/.ssh/archiquan_site_deploy
git remote set-url origin git@github.com:archiquan/archiquan.github.io.git
git config core.sshCommand "ssh -i ~/.ssh/archiquan_site_deploy -o IdentitiesOnly=yes"
```

- Copy the public half for the user (`pbcopy < ~/.ssh/archiquan_site_deploy.pub`). The user adds it at
  github.com/archiquan/archiquan.github.io/settings/keys/new with **Allow write access** ticked.
- Before the first push, check that GitHub's ed25519 host key fingerprint is
  `SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU` (`ssh-keyscan -t ed25519 github.com`), then
  add it to `~/.ssh/known_hosts`.
- Never ask for or type the user's GitHub password or a token.

## Content rules

- Paper titles and one-line summaries follow the user's latest CV or cover letter. If they disagree
  with each other, ask which one wins.
- The "Highest Exam" in the gaokao paper's subtitle was the user's deliberate choice. Keep it.
- Give no journal or "under review" status for any paper unless the user states its current status.
- The E100 line shows "Average student rating 4.42/5": the mean of the five item means in the
  Michaelmas 2025–26 survey (4.50, 4.40, 4.60, 4.20, 4.40; 10 responses), plus its 90% satisfaction
  ratio. Recompute it the same way if a new survey is added.
- The CV section and footer still say "Last updated: June 2026". Update them whenever the CV
  section's content changes.
