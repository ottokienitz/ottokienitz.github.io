# Editing Guide — ottokienitz.github.io

## Site Overview

This site is built with **R Markdown** (`.Rmd` files) using Bootstrap 3 and hosted on GitHub Pages at www.ottokienitz.com. Each `.Rmd` file compiles to an `.html` file. The navbar, theme, and output settings are controlled by `_site.yml`.

### Key Files

| File | Page |
|------|------|
| `_site.yml` | Site config: navbar, theme, output settings |
| `index.Rmd` | Home page |
| `research.Rmd` | Research (book, papers, theses) |
| `cv.Rmd` | Curriculum Vitae |
| `statecap.Rmd` | Sample syllabus: State Capacity and Public Policy |
| `resources.Rmd` | Resources (CP, Russia/Eurasia, Data, Recommendations) |
| `rsd.Rmd` | Russian State and Democracy syllabus (2023) |
| `ee.Rmd` | Eastern European Politics syllabus |
| `ps2_s20.Rmd` / `ps2_s19.Rmd` | Comparative Politics syllabi |
| `ps3.Rmd` | Quantitative Methods syllabus |
| `styles.css` | Custom CSS (typography, colors, layout) |

---

## Markdown Syntax Reference

### Text Formatting

| What you want | Syntax | Result |
|---|---|---|
| Bold | `**text**` or `__text__` | **text** |
| Italic | `*text*` or `_text_` | *text* |
| Bold + Italic | `***text***` or `___text___` | ***text*** |
| Inline code | `` `code` `` | `code` |

### Citation Conventions (Research Page)

- **Book / dissertation / thesis titles** — bold italic, no quotes: `___Title Here___`
- **Paper titles** — bold with quotation marks: `__"Title Here"__`
- **Journal names** — italic: `*Annual Review of Political Science*`
- **Book titles in running text** — italic: `*Kings as Judges*`

### Links

```markdown
[display text](https://example.com)
[email me](mailto:okienit1@jhu.edu)
```

### Images

```html
<img align="center" src="images/filename.jpg" width="500">

*Caption text in italics*
```

Images go in the `images/` folder. Use `align="right"` for text wrapping (used on the home page).

### Headings

```markdown
# Heading 1 (page title — set in YAML, rarely used in body)
## Heading 2 (tab names when inside a tabset)
### Heading 3 (section headers)
#### Heading 4 (item titles — papers, weekly topics)
```

### Horizontal Rules

```markdown
---
```

A line with just three dashes creates a divider. Used between sections throughout the site.

### Lists

```markdown
* Bullet item
* Another item

1. Numbered item
2. Another item
```

### Blockquotes

```markdown
> Indented text (used for "Additional resources" in syllabi)
```

### Tabs

```markdown
# {.tabset .tabset-fade}

## First Tab

Content for first tab...

## Second Tab

Content for second tab...
```

The `# {.tabset .tabset-fade}` line triggers tab layout. Each `##` heading becomes a tab. Used on the Resources page and some syllabi.

### Collapsible Sections

```html
<details>
<summary>Click to expand</summary>

Content here (leave a blank line after the summary tag)

</details>
```

Used on the Research page for the dissertation table of contents.

### Styled Week Headers (Syllabi)

```html
<h4>*Week 1: Topic Title*</h4>
```

This gives italicized week headers at the h4 size. Used in `statecap.Rmd` and other syllabi.

---

## YAML Front Matter

Every `.Rmd` file starts with a YAML block:

```yaml
---
title: "Page Title"
---
```

The title appears as the page heading. Don't change this unless you want to rename the page.

---

## Editing the Navbar

Open `_site.yml` to add/remove/reorder pages in the navigation bar.

```yaml
navbar:
  left:
    - text: "Display Name"
      href: filename.html
    - text: "Dropdown Menu"
      menu:
      - text: "Item 1"
        href: page1.html
      - text: "Item 2"
        href: page2.html
```

To add a new page: create a new `.Rmd` file, then add an entry in `_site.yml`.

---

## Building the Site

### From RStudio (recommended)

1. Open `ottokienitz.github.io.Rproj` in RStudio
2. Go to the **Build** tab (top-right pane)
3. Click **Build Website** to rebuild everything
4. Or open a single `.Rmd` file and click **Knit** to rebuild just that page

### From Terminal

```bash
cd /Users/ojk/Documents/Websites/ottokienitz.github.io

# Rebuild a single page:
Rscript -e "Sys.setenv(RSTUDIO_PANDOC='/Applications/RStudio.app/Contents/Resources/app/quarto/bin/tools/aarch64'); rmarkdown::render('statecap.Rmd')"

# Rebuild the entire site:
Rscript -e "Sys.setenv(RSTUDIO_PANDOC='/Applications/RStudio.app/Contents/Resources/app/quarto/bin/tools/aarch64'); rmarkdown::render_site()"
```

The `RSTUDIO_PANDOC` path is needed when running from Terminal because pandoc isn't on the system PATH. RStudio handles this automatically.

After building, open the `.html` file in a browser to preview before pushing.

---

## Pushing to GitHub

### From RStudio

1. Go to the **Git** tab (top-right pane)
2. Check the boxes next to changed files to stage them
3. Click **Commit**, write a message, click **Commit**
4. Click **Push** (the green up arrow)

### From Terminal

```bash
cd /Users/ojk/Documents/Websites/ottokienitz.github.io

# 1. Check what changed
git status

# 2. Stage all changes
git add -A

# 3. Commit with a message
git commit -m "Description of what changed"

# 4. Push to GitHub
git push origin main
```

Changes go live at www.ottokienitz.com within a minute or two after pushing.

---

## Common Tasks

### Add a new working paper

Edit `research.Rmd`. Under the `### Working Papers` section, add:

```markdown
---

#### __"Paper Title Here"__ (with [Coauthor Name](https://coauthor-url.com))

Optional one-line description.
```

### Add a new course syllabus

1. Create a new `.Rmd` file (e.g., `newcourse.Rmd`) in the site root
2. Add YAML front matter with `title: "Course Name"`
3. Add the entry to the Teaching dropdown in `_site.yml`
4. Build and push

### Update the CSS

Edit `styles.css`. Changes apply to all pages on the next build. Key sections:
- Typography (font, line-height, heading sizes)
- Links (color, hover effects)
- Navbar (background color, hover states)
- Images (border-radius, shadows)
- Tabs (active state styling)
- Responsive/mobile adjustments (`@media` block at the bottom)
