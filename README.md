# Blessington Educate Together website

This repository contains the files for the Blessington Educate Together school website.

The site was rebuilt from the former WordPress website as a static Hugo site and is published using GitHub Pages. Most ordinary updates can be made directly in GitHub by editing text files or uploading files such as PDFs and images.

For technical notes about Hugo, deployment, and the original WordPress conversion, see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## What can be updated here

This README is intended for simple website updates, such as:

- updating text on an existing page
- changing teacher names, class names, or school information
- adding or replacing a PDF, such as the school calendar
- adding a picture to a page
- adding a simple new page

For larger changes, layout changes, menu changes, or technical problems, ask for help.

---

## The most important folders and files

| Folder or file | What it is for |
|---|---|
| `content/` | Website pages and page text |
| `static/uploads/documents/` | PDFs and other downloadable documents |
| `static/uploads/images/` | Images added to pages |
| `CONTRIBUTING.md` | Technical notes for developers |

Most routine updates only need `content/`, `static/uploads/documents/`, and `static/uploads/images/`.

---

## How changes go live

Changes can be made directly on the `main` branch.

When a change is saved to the `main` branch, GitHub automatically rebuilds and publishes the website.

After saving a change, the update may not appear on the live site immediately. GitHub needs to finish rebuilding the site first.

If the site does not update or something looks wrong, ask for help.

---

## Editing in github.dev

For a more comfortable editing view, open the repository at:

```text
https://github.dev/betns/betns-ie
```

This opens the website files in a browser-based editor.

This can be easier than editing one file at a time on GitHub, especially when updating page text or checking several files. Save changes by committing them to the `main` branch.

For uploading PDFs or images, it may still be easiest to use the normal GitHub website.

---

## Editing text on an existing page

Website pages are stored in the `content/` folder.

Most pages have their own folder containing an `index.md` file, for example:

```text
content/contact-us/index.md
content/about-us/index.md
```

To edit page text:

1. Open the relevant page folder inside `content/`.
2. Open `index.md`.
3. Click the edit button in GitHub.
4. Edit the text in the file.
5. Save or commit the change to the `main` branch.

Many pages begin with a small settings section at the top, for example:

```toml
+++
title = "Contact Us"
weight = 10
+++
```

Try not to change this top section unless you are changing the page title.

The normal page text appears below that section.

---

## Basic formatting

The site uses Markdown for most page content.

### Paragraphs

Leave a blank line between paragraphs.

```markdown
This is one paragraph.

This is another paragraph.
```

### Headings

```markdown
## This is a heading
```

### Bullet lists

```markdown
- First item
- Second item
- Third item
```

### Links

```markdown
[Visit Educate Together](https://www.educatetogether.ie/)
```

### Links to files on this site

```markdown
[Download the school calendar](/uploads/documents/school-calendar-2026-2027.pdf)
```

---

## Adding or updating a PDF

PDFs and other downloadable files should go in:

```text
static/uploads/documents/
```

Use simple file names with lowercase letters and hyphens, for example:

```text
school-calendar-2026-2027.pdf
booklist-first-class.pdf
policy-admissions.pdf
```

Avoid spaces in file names.

### Updating the school calendar PDF

The school calendar is a good example of a document that may need to be updated every year.

To update it:

1. Upload the new calendar PDF to `static/uploads/documents/`.
2. Use a clear file name, for example:

```text
school-calendar-2026-2027.pdf
```

3. Open the page where the school calendar is linked.
4. Update the link so that it points to the new PDF:

```markdown
[Download the school calendar](/uploads/documents/school-calendar-2026-2027.pdf)
```

5. Save or commit the change to the `main` branch.

### Replacing an existing PDF

There are two simple options.

Option 1: upload the new PDF using the same file name as the old PDF.

This keeps the existing website link working.

Option 2: upload the new PDF with a new file name, then update the link on the relevant page.

For annual documents, a new file name is usually clearer, for example:

```text
school-calendar-2026-2027.pdf
```

---

## Adding a picture to a page

Images should go in:

```text
static/uploads/images/
```

Use simple file names with lowercase letters and hyphens, for example:

```text
junior-infants-classroom.jpg
school-garden.jpg
active-schools-week.jpg
```

Avoid spaces in file names.

To add an image to a page, upload the image and then add this to the page text:

```markdown
![Children working in the school garden](/uploads/images/school-garden.jpg)
```

The text inside the square brackets describes the image. This is useful for accessibility and for people using screen readers.

### Useful image layouts

The site supports a few simple image layout options.

| Markdown | Effect |
|---|---|
| `![Description](/uploads/images/photo.jpg)` | Normal image |
| `![Description](/uploads/images/photo.jpg#center)` | Centred image |
| `![Description](/uploads/images/photo.jpg#thumb)` | Smaller image with text wrapping around it |
| `![Description](/uploads/images/photo.jpg#banner)` | Wide banner-style image |

Example:

```markdown
![School garden](/uploads/images/school-garden.jpg#center)
```

With a caption:

```markdown
![School garden](/uploads/images/school-garden.jpg#center "Our school garden")
```

---

## Adding a simple new page

To add a simple new page:

1. Go to the `content/` folder.
2. Create a new folder with a simple lowercase name, for example:

```text
content/school-calendar/
```

3. Inside that folder, create a file called:

```text
index.md
```

4. Add this starter content:

```markdown
+++
title = "School Calendar"
weight = 50
+++

Add the page text here.
```

The page will be available at:

```text
/school-calendar/
```

For example, a page in:

```text
content/school-calendar/index.md
```

will appear on the website as:

```text
/school-calendar/
```

A new page is not automatically added to the main menu. Ask for help if the new page should appear in the website menu.

---

## When to ask for help

Ask for help before making changes to:

- the website design or layout
- the main navigation menu
- the contact form
- technical files such as `.github/`, `layouts/`, `scripts/`, `hugo.toml`, or `CONTRIBUTING.md`
- anything involving the old WordPress site
- anything that causes the site build to fail

For routine text edits, PDF updates, images, and small new pages, the steps above should be enough.