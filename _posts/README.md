Totally get the confusion—“Recent posts” isn’t a tab you turned on; it’s coming from the **home page layout**.

Here’s how Minimal Mistakes handles it and how you can control it:

# Why you see “Recent posts”

* Your `index.md` (or `index.html`) at the site root is probably using `layout: home`.
* The **`home`** layout automatically inserts the *Recent posts* section (and uses pagination if `_config.yml` has `paginate:` set).

# Hide/remove the Recent Posts section (keep a simple Home)

Edit (or create) `index.md` at the project root like this:

```yaml
---
layout: single   # or "splash" if you want a hero-style landing
title: "Home"
permalink: /
author_profile: false   # hides the left author box if you don’t want it
---
Welcome to my website.
```

Also, in `_config.yml`, either remove or comment out `paginate:` (it only matters for `layout: home`, but good to keep it off if you don’t use a blog):

```yaml
# paginate: 5   # comment out or remove
```

# Where the top navigation “tabs” come from

They’re defined in `_data/navigation.yml`. For a simple set of tabs:

```yaml
# _data/navigation.yml
main:
  - title: "Home"
    url: /
  - title: "Research and Projects"
    url: /research/
  - title: "Teaching"
    url: /teaching/
  - title: "Besides Work"
    url: /besides/
  - title: "CV"
    url: /cv/
  # (No Blog/Posts link if you don’t want a blog tab)
```

# If you *do* want to post later: how to create posts

1. Make sure you have a folder called `_posts/`.
2. Add Markdown files named like `YYYY-MM-DD-your-title.md`.
3. Each post needs front matter. Example:

   ```yaml
   ---
   title: "My first post"
   date: 2025-10-01
   layout: single     # common for posts in Minimal Mistakes
   categories: [notes]   # optional
   tags: [research, teaching]  # optional
   ---
   Your post content here...
   ```
4. If you want a **Blog** tab that lists posts, create a page (e.g., `blog.md`) with:

   ```yaml
   ---
   title: "Blog"
   layout: posts      # this layout shows the post index
   permalink: /blog/
   ---
   ```

   Then add a link to it in `_data/navigation.yml`:

   ```yaml
   - title: "Blog"
     url: /blog/
   ```

# Optional: keep author box but no recent posts

* Use `layout: single` on `index.md`.
* Set `author_profile: true` if you want the profile column on the left:

  ```yaml
  ---
  layout: single
  title: "Home"
  permalink: /
  author_profile: true
  ---
  ```

# Quick checklist for your case

* Change `index.md` → `layout: single` (or `splash`).
* Set `author_profile: false` if you don’t want the left column.
* Remove `paginate:` from `_config.yml`.
* Make sure `_data/navigation.yml` only lists the tabs you want.

If you paste your current `index.md` and `_config.yml` snippets, I can give you the exact minimal edits.
