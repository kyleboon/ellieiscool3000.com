# Ellie Is Cool 3000

The website at **ellieiscool3000.com**. Plain HTML and CSS — no build step, no
dependencies, no framework. Edit a file, push, done.

---

## Getting it onto GitHub Pages

```bash
cd ellieiscool3000
git init
git add .
git commit -m "Start the site"
gh repo create ellieiscool3000 --public --source=. --push
```

Then repo → **Settings** → **Pages** → Source: *Deploy from a branch* → Branch
`main`, folder `/ (root)`.

Without the `gh` CLI, make the empty repo in the browser first, then:

```bash
git remote add origin https://github.com/YOURUSER/ellieiscool3000.git
git branch -M main
git push -u origin main
```

## Pointing the domain at it

A `CNAME` file containing `ellieiscool3000.com` is already in this folder, so
pushing it sets the custom domain automatically — you shouldn't need to type
anything into the Pages settings box.

At your registrar, create four A records on the apex (`@`):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

And four AAAA records, for IPv6:

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

Then a CNAME record so the www version works too:

```
www  →  YOURUSER.github.io
```

Delete any parking/placeholder record the registrar added when you bought the
domain, or it will fight with these.

DNS can take up to 24 hours, though it's usually minutes. Once it resolves, go
back to Settings → Pages and tick **Enforce HTTPS**. That box stays greyed out
until GitHub has issued the certificate, so if it's not clickable yet, wait and
come back.

**One gotcha given you already run Pages sites:** an apex domain can only be
attached to one repository at a time. If `ellieiscool3000.com` is currently
pointed at anything else of yours, that has to be released first.

## Previewing before pushing

Double-clicking `index.html` works. Or:

```bash
python3 -m http.server 8000
```

## A note on photos

The repo is public, so anything committed is public and stays in the git
history even if deleted later. Photos taken on a phone can carry GPS
coordinates in their EXIF data — worth stripping before committing pictures of
her artwork:

```bash
exiftool -all= images/*.jpg
```

Scans and screenshots don't have this problem.

---

## For her

Everything below is written for Ellie. Worth reading through together once.

### The files

| File | What's in it |
|---|---|
| `index.html` | the front page |
| `stories.html` | all the stories |
| `poems.html` | all the poems |
| `art.html` | all the pictures |
| `style.css` | the colors and fonts |
| `images/` | where picture files live |
| `favicon.svg` | the tiny star that shows up in the browser tab |
| `CNAME` | tells GitHub the address of the site — leave this one alone |

### Adding a poem

Open `poems.html`. Find the part that says **TO ADD A POEM**. Copy the block
underneath it — everything from `<article class="card">` down to
`</article>` — and paste it right below. Then change the title and type your
poem in.

Line breaks just work. Press Enter where you want a new line.

### Adding a story

Same idea in `stories.html`. Each paragraph needs `<p>` at the start and
`</p>` at the end. That's what tells the computer where paragraphs stop.

### Adding a picture

1. Put the picture file in the `images` folder.
2. Name it with lowercase letters and dashes instead of spaces —
   `blue-dragon.png`, not `Blue Dragon (final!!).png`.
3. In `art.html`, copy a `<figure>` block and paste it below the others.
4. Change `images/placeholder-1.svg` to `images/blue-dragon.png`.
5. Change the title and the little note underneath.

The `alt="..."` part is a description of the picture, for people who use a
screen reader and can't see it. Write what's actually in the picture.

### Changing the colors

Open `style.css`. The colors are all at the very top, with names:

- `--punch` is the hot pink on the front page and the art page
- `--watermelon` is the pinky-red on the stories page
- `--orchid` is the purpley-pink on the poems page
- `--paper` is the background of every page

Change a hex code, save, refresh. If it goes horribly wrong,
`git checkout style.css` puts it back exactly how it was.

Each `--accent-deep` is the darker version of a color, used behind white text
so it stays easy to read. If you change a bright color, nudge its deep one the
same direction.

### Rules of thumb

- Every tag that opens has to close. `<h2>` needs `</h2>`.
- Don't delete the `class="..."` bits — those are what make things look right.
- Save, then refresh the browser to see the change.
- If something breaks, undo until it works again. Nothing here is permanent.
