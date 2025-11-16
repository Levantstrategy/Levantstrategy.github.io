# Using Jekyll Partials on GitHub Pages

## Overview

Your website now has Jekyll configured with reusable partials! This means you can share common code (navigation, footer, head) across all pages.

## Structure

```
_config.yml               # Jekyll configuration
_layouts/
  └── default.html        # Main layout template
_includes/
  ├── head.html          # <head> section with meta tags, CSS
  ├── navigation.html    # Navigation bar
  └── footer.html        # Footer with contact info
```

## How to Use

### Option 1: Using Layouts (Recommended)

Convert your HTML pages to use the layout. Here's how:

**Before (old aboutus.html):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- ... all the head content ... -->
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar...">
        <!-- ... full navbar ... -->
    </nav>

    <!-- Your page content -->
    <section>...</section>

    <!-- Footer -->
    <footer>...</footer>
</body>
</html>
```

**After (new aboutus.html):**
```html
---
layout: default
title: About Us
---

<!-- Your page content only -->
<section class="hero" style="padding: 6rem 0 4rem;">
    <div class="container">
        <!-- ... your content ... -->
    </div>
</section>

<section class="section">
    <!-- ... more content ... -->
</section>
```

The `---` section at the top is called "Front Matter" and tells Jekyll to use the default layout.

### Option 2: Using Includes Directly

If you prefer not to use layouts, you can use includes in any HTML page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    {% include head.html %}
</head>
<body>
    {% include navigation.html %}

    <!-- Your page content -->
    <section>...</section>

    {% include footer.html %}
</body>
</html>
```

## Converting Your Pages

To convert a page like `aboutus.html`:

1. **Extract the content**: Copy only the main content sections (everything between `<body>` tags, excluding navigation and footer)

2. **Add front matter**: At the very top of the file, add:
   ```yaml
   ---
   layout: default
   title: Your Page Title
   ---
   ```

3. **Paste content**: Add your page content below the front matter

4. **Done!** The layout will automatically add the navigation, footer, and all necessary HTML structure

## Benefits

✅ **Update once, apply everywhere**: Change navigation in one file, updates all pages
✅ **Cleaner code**: Each page only contains its unique content
✅ **Easier maintenance**: No need to copy/paste common elements
✅ **Native GitHub Pages support**: Works automatically on GitHub Pages

## Testing Locally (Optional)

To test Jekyll locally before pushing:

```bash
# Install Jekyll (one-time setup)
gem install jekyll bundler

# Create Gemfile
echo 'source "https://rubygems.org"' > Gemfile
echo 'gem "github-pages", group: :jekyll_plugins' >> Gemfile

# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Visit http://localhost:4000
```

## Important Notes

- Jekyll processes files on GitHub Pages automatically - no build step needed!
- Keep `.html` extensions for your files
- The `_config.yml`, `_includes/`, and `_layouts/` directories are special Jekyll folders
- Changes to `_config.yml` require restarting the local server (if testing locally)
- On GitHub Pages, changes take 1-2 minutes to rebuild

## Example Conversion

See `aboutus-example.html` for a complete example of a converted page.

