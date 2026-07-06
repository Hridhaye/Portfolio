# Site Guide — writing, editing & publishing

Everything on this site is built from **one file: `articles.json`**. You edit
articles using the **Article Manager** (`admin.html`), download the updated
`articles.json`, and push it. The homepage, the archive, and each article page
all update from that single file — you never hand-edit HTML to publish.

---

## 1. Opening the Article Manager

The Manager needs to *load* `articles.json`, and browsers block that when you
open the file by double-clicking (a `file://` security rule). So use **one** of:

- **Easiest:** open the published page — `https://<your-site>/admin.html`.
- **Local:** in this folder run `python -m http.server 8000`, then open
  `http://localhost:8000/admin.html`.
- **Fallback:** if you did double-click the file, click **⤒ Load articles.json**
  in the top bar and pick `articles.json` manually.

When it opens it automatically loads your current articles into the left-hand list.

---

## 2. Adding a new article

1. Click **+ New** (top of the left list).
2. Fill in the fields:
   - **Filename (slug)** — lowercase, no spaces (e.g. `my-new-piece`). This becomes
     the article's web address: `article.html?slug=my-new-piece`. **Don't change a
     slug after sharing the link** — it would break the old URL.
   - **Title** — wrap words in `*asterisks*` to make them green italic.
   - **Dek** — the one-line italic subtitle.
   - **Category, Year** — Year is used for your own reference; it is **not** shown
     as a date on the site.
   - **Date / Read time** — optional. Shown in the article byline only. Leave blank
     if you don't want them.
   - **Body** — write in Markdown, and drop in images wherever you like (see section 6).
3. Click **✓ Save to list**. The piece now appears in the left list and in both previews.
4. Repeat for any other changes, then **publish** (section 4).

---

## 3. Editing or deleting an article

- **Edit:** click any article in the left list. It loads into the form. Make changes,
  then click **✓ Save to list**.
- **Delete:** hover an item in the list and click the **✕**, or open it and click
  **Delete this**. You'll be asked to confirm.

Nothing is permanent until you download and push the file (section 4).

---

## 4. Publishing your changes

1. Click **⬇ Download articles.json** (top bar). A new `articles.json` downloads.
2. Replace the old `articles.json` in this project folder with the downloaded one.
3. Commit and push:
   ```
   git add articles.json
   git commit -m "Add/update article"
   git push
   ```
4. GitHub Pages redeploys in a minute or two, and every page updates at once.

> Your work is saved in the browser between sessions, so closing the tab won't
> lose anything. But it only goes **live** after you download + push the file.

---

## 5. Controlling the order of articles

The order of articles in the Manager's left-hand list **is** the order they appear on
the site — the writing archive (`writing.html`) lists them top to bottom, and the
homepage's "Selected Writing" shows the first few.

**To rearrange:** hover an article in the left list and use the **▲ / ▼** buttons
(bottom-right of the card) to move it up or down. As with any change, it only goes live
after you **Download articles.json** and push (section 4).

---

## 6. Writing the body (Markdown & images)

The **Body** field uses Markdown. The toolbar buttons insert the syntax for you, but
here's what's supported:

| You write | You get |
|-----------|---------|
| `## Heading` | A section heading |
| `### Smaller heading` | A sub-heading |
| `**bold**` | **bold** |
| `*italic*` | *italic* |
| `H<sub>2</sub>O` | subscript (use the **x₂** button) |
| `x<sup>2</sup>` | superscript (use the **x²** button) |
| `[text](https://url.com)` | a link |
| `- item` (one per line) | a bulleted list |
| `1. item` (one per line) | a numbered list |
| `> A line` | a **pull quote** with the green accent rule |
| `***` (on its own line) | a `• • •` section break |

Leave a blank line between paragraphs. The first paragraph automatically gets the
large drop-cap.

**Pasting text.** When you paste prose, paragraph spacing is added for you — you don't
need to go through and insert blank lines between paragraphs by hand. Lists, headings,
and quotes you paste keep their own formatting.

**Lists.** Select the lines you want and click **• List** (bullets) or **1. List**
(numbered) — numbers are filled in for you and always stay in order, even if you add or
remove items later. When you **paste** a bulleted or numbered list (from Word, Google
Docs, the web, etc.), its list formatting is kept automatically.

**Subscript & superscript:** select text and click the **x₂** or **x²** toolbar button,
or type the tags directly. You can also **paste text that already contains sub/superscript**
(from Word, the web, a PDF, etc.) — it's preserved automatically, including characters like
`x²` or `CO₂`.

### Inserting images

Put your cursor where you want the image, then either:

- click **🖼 Insert image** and pick a file, **or**
- **paste an image directly** into the body — a screenshot (e.g. after Win+Shift+S), a
  right-click "copy image" from a web page, or a copied image file. No need to save it
  anywhere first.

Either way you'll be asked for an optional caption — type one (it appears in small grey
text under the image) or leave it blank. You can add **as many images as you like,
anywhere** in the article, just like Substack.

- The image is embedded straight into `articles.json`, so there are no separate image
  files to manage or upload.
- **Images are automatically resized and compressed** on insert (capped at 1200 px
  wide, re-encoded as JPEG unless they have transparency). The toast tells you the final
  size — you don't need to shrink images yourself. If one is still large after that,
  you'll get a heads-up before it's added.

**Editing images after inserting.** To keep the editor readable, each image shows as a
short tag like `![your caption](@img1)` — **not** a giant blob of image data. To:

- **change or add a caption** — put your cursor on the image's tag and click
  **✎ Edit caption** (or just retype the text between the `![ ]`);
- **resize an image** — put your cursor on its tag and click **⇔ Resize image**. It
  asks two things: a **width** as a percent of the column (10–100; 100 = full width),
  and an optional **max height** in pixels (leave blank for none). Height keeps the
  image's proportions — it just stops a tall image from getting too big. The image is
  centered at the size you choose;
- **move an image** — cut and paste its whole `![…](@img1)` tag to a new spot;
- **delete an image** — delete its whole `![…](@img1)` tag.

The real image data is stitched back in automatically when you Save, so the downloaded
`articles.json` always contains the full image.

---

## 7. Editing articles.json directly (optional)

You never *have* to touch this file, but it's plain text if you prefer. Each article
is one entry:

```json
{
  "slug": "my-piece",
  "title": "My *green-accented* title",
  "dek": "One-line subtitle.",
  "category": "Politics & Policy",
  "year": "2025",
  "date": "October 2025",
  "readtime": "8 min read",
  "body": "Markdown text.\n\n## A heading\n\n> A pull quote.\n\n![A caption](data:image/...)"
}
```

- `\n` means a line break inside the body text.
- Images live inside `body` as `![caption](data:image/...)` — always add them via the
  Manager's **🖼 Insert image** button, which generates that data for you.
- Keep the commas and quotes intact — if the JSON is malformed the site can't load it.
  (The Manager always writes valid JSON, which is why it's the safer path.)

---

## 8. The files, at a glance

| File | What it is |
|------|-----------|
| `articles.json` | All article content. The one file you edit to publish. |
| `admin.html` | The Article Manager (add / edit / delete / export). |
| `article.html` | Renders one article, e.g. `article.html?slug=clean-grid`. |
| `index.html` | Homepage. |
| `writing.html` | The archive list. |
| `clean-grid.html`, `barbenheimer.html`, `istanbul.html` | Original standalone pages, kept only so old links don't break. Nothing on the site links to them now; safe to delete. |

---

## Quick reference

**To publish anything:** edit in `admin.html` → **Download articles.json** →
replace the file → `git add articles.json && git commit -m "..." && git push`.
