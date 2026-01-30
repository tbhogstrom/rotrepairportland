# Site Clone Process: rotrepairseattle.com → rotrepairportland.com

This document describes the process used to clone and rebrand the Seattle rot repair site for the Portland market.

## Overview

| Original Site | New Site |
|---------------|----------|
| rotrepairseattle.com | rotrepairportland.com |
| SFW Construction | SFW Construction (same) |
| (206) 539-1785 | (503) 885-0236 |
| 4500 9th Ave NE, Suite 300, Seattle, WA | 2552 NW Vaughn St., Portland, OR 97210 |
| WA License | OR CCB# 166405 \| WA LIC# SFWCOC*745 |

---

## Step 1: Download Source Site

Since `wget` wasn't available, we used `curl` to download pages based on the sitemap.

### Discover Site Structure
```bash
# Get sitemap index
curl -s https://rotrepairseattle.com/sitemap_index.xml

# Get page URLs from sitemaps
curl -s https://rotrepairseattle.com/page-sitemap.xml
curl -s https://rotrepairseattle.com/post-sitemap.xml
```

### Download All Pages
```bash
#!/bin/bash
PAGES=(
    "https://rotrepairseattle.com/"
    "https://rotrepairseattle.com/free-rot-repair-estimate/"
    "https://rotrepairseattle.com/home/"
    "https://rotrepairseattle.com/blog/"
    "https://rotrepairseattle.com/contact-us-2/"
    "https://rotrepairseattle.com/the-hidden-costs-of-dry-rot/"
    "https://rotrepairseattle.com/the-lifecycle-of-dry-rot/"
    "https://rotrepairseattle.com/permanent-rot-repair-solution/"
    "https://rotrepairseattle.com/detecting-and-managing-rot-in-your-home/"
    "https://rotrepairseattle.com/how-to-identify-dry-rot-on-your-home/"
    "https://rotrepairseattle.com/seattle-flat-roof-repairs/"
    "https://rotrepairseattle.com/why-do-your-windows-leak-when-it-rains/"
    "https://rotrepairseattle.com/dry-rot-repair-cost-seattle/"
)

for url in "${PAGES[@]}"; do
    filename=$(echo "$url" | sed 's|https://rotrepairseattle.com/||' | sed 's|/$||')
    [[ -z "$filename" ]] && filename="index"
    curl -s -L "$url" -o "source/pages/${filename}.html"
    sleep 1
done
```

---

## Step 2: Content Transformation

### Python Transformation Script (`transform.py`)

The transformation script handles multiple replacement categories:

#### Domain Replacements
```python
("rotrepairseattle.com", "rotrepairportland.com"),
("rotrepairseattle", "rotrepairportland"),
```

#### Phone Number Replacements
```python
("206-539-1785", "(503) 885-0236"),
("(206) 539-1785", "(503) 885-0236"),
("2065391785", "5038850236"),
("tel:206-539-1785", "tel:503-885-0236"),
```

#### Address Replacements
```python
("4500 9th Ave NE Suite 300 Seattle, WA", "2552 NW Vaughn St., Portland, OR 97210"),
("4500 9th Ave NE, Suite 300", "2552 NW Vaughn St."),
("4500 9th Ave NE", "2552 NW Vaughn St."),
```

#### Geographic Replacements
```python
("Seattle, WA", "Portland, OR"),
("Seattle, Washington", "Portland, Oregon"),
("Greater Seattle area", "Greater Portland area"),
("Seattle metro area", "Portland metro area"),
("King County", "Multnomah County"),
("Puget Sound", "Willamette Valley"),
("Seattle's", "Portland's"),
("Seattle", "Portland"),
```

#### URL Slug Replacements
```python
("seattle-flat-roof-repairs", "portland-flat-roof-repairs"),
("dry-rot-repair-cost-seattle", "dry-rot-repair-cost-portland"),
```

#### Anchor/ID Replacements
```python
("h-seattle-weather-and-dry-rot", "h-portland-weather-and-dry-rot"),
("h-seattle-s-climate-makes-it-worse", "h-portland-s-climate-makes-it-worse"),
# ... and many more
```

### Important: Preserve CDN Image URLs

The original site uses NitroPack CDN for images. These URLs must **NOT** be transformed:

```
https://cdn-ileeamj.nitrocdn.com/WrsmSvzGThHeWebWzpPigJcevuotdycK/assets/images/optimized/rev-26df6f7/rotrepairseattle.com/wp-content/uploads/...
```

The `rotrepairseattle.com` in the CDN path must stay as-is because that's where the actual images exist.

**Do NOT transform:**
- Image filenames containing "seattle" (e.g., `dry-rot-seattle.webp`)
- CDN domain paths

---

## Step 3: Generate Service Area Pages

Created 39 location-specific pages for Portland metro area SEO:

### Portland Neighborhoods
- NE Portland, SE Portland, NW Portland, SW Portland, N Portland
- Hawthorne, Alberta Arts, Sellwood, Irvington, Mt. Tabor
- Pearl District, St. Johns, Foster-Powell, Division, Montavilla
- Laurelhurst, West Hills

### Surrounding Cities
- Beaverton, Hillsboro, Gresham, Lake Oswego, Oregon City
- Milwaukie, Tigard, Tualatin, West Linn, Wilsonville
- Happy Valley, Clackamas, Forest Grove, Aloha
- Cedar Hills, Cedar Mill, Troutdale, Fairview, Wood Village
- Sherwood, King City, Durham

### Service Area Page Template
Each page includes:
- Location-specific title and meta description
- Schema.org LocalBusiness markup
- Service list
- Contact information
- CCB license number

---

## Step 4: Vercel Configuration

Create `vercel.json` for clean URLs:

```json
{
  "cleanUrls": true,
  "trailingSlash": false,
  "rewrites": [
    { "source": "/category/:path*", "destination": "/blog" },
    { "source": "/tag/:path*", "destination": "/blog" },
    { "source": "/feed", "destination": "/blog" },
    { "source": "/feed/", "destination": "/blog" }
  ]
}
```

This allows URLs like `/blog` to serve `blog.html`.

---

## Step 5: Deploy to GitHub

```bash
cd output
git init
git remote add origin https://github.com/tbhogstrom/rotrepairportland.git
git add -A
git commit -m "Initial site build"
git branch -M main
git push -u origin main
```

Connect repo to Vercel for automatic deployment.

---

## File Structure

```
output/
├── index.html                              # Homepage
├── home.html                               # Alternate home
├── blog.html                               # Blog listing
├── contact-us-2.html                       # Contact page
├── free-rot-repair-estimate.html           # Lead capture form
├── portland-flat-roof-repairs.html         # Flat roof services
├── dry-rot-repair-cost-portland.html       # Pricing/cost guide
├── permanent-rot-repair-solution.html      # Blog post
├── the-hidden-costs-of-dry-rot.html        # Blog post
├── the-lifecycle-of-dry-rot.html           # Blog post
├── detecting-and-managing-rot-in-your-home.html  # Blog post
├── how-to-identify-dry-rot-on-your-home.html     # Blog post
├── why-do-your-windows-leak-when-it-rains.html   # Blog post
├── service-areas/                          # 39 location pages
│   ├── ne-portland.html
│   ├── se-portland.html
│   ├── beaverton.html
│   └── ... (36 more)
├── service-areas-sitemap.xml               # Sitemap for locations
├── vercel.json                             # Vercel config
├── DEPLOYMENT_GUIDE.md                     # Deployment checklist
└── CLONE_PROCESS.md                        # This file
```

---

## Known Limitations

### Static HTML Site
This is a static HTML export, not a WordPress installation:
- No admin panel
- Forms don't submit (need Formspree, Netlify Forms, etc.)
- No dynamic content
- No commenting system

### Images
Images load from the original NitroPack CDN at `rotrepairseattle.com`. This works because CDNs don't restrict by requesting domain, but:
- If the Seattle site goes down, images break
- For full independence, download and re-host images

### Forms
Contact and estimate forms need a backend service:
- [Formspree](https://formspree.io/)
- [Netlify Forms](https://www.netlify.com/products/forms/)
- [Basin](https://usebasin.com/)

---

## QA Verification

Run the QA script to check for missed replacements:

```bash
python3 qa_verify.py
```

Checks for:
- ❌ Old phone number (206-539-1785)
- ❌ Old domain (rotrepairseattle.com) in non-CDN contexts
- ❌ Old address (4500 9th Ave NE)
- ❌ King County references
- ✅ New phone number
- ✅ New domain
- ✅ Business name
- ✅ License numbers

---

## Future Improvements

1. **Download and self-host images** - Remove dependency on Seattle CDN
2. **Set up form handling** - Integrate Formspree or similar
3. **Add Google Analytics** - New property for Portland site
4. **Google Business Profile** - Create listing for Portland location
5. **Unique content** - Rewrite introductions to avoid duplicate content penalties
6. **Local photos** - Add Portland-specific project photos
7. **Testimonials** - Add Portland customer reviews

---

## Scripts Reference

| Script | Purpose |
|--------|---------|
| `transform.py` | Main content transformation |
| `generate_service_areas.py` | Create location pages |
| `qa_verify.py` | Verify no old references remain |
| `download_site.sh` | Download source pages |

---

## Contact

Site built for **SFW Construction**
- Phone: (503) 885-0236
- Address: 2552 NW Vaughn St., Portland, OR 97210
- License: OR CCB# 166405 | WA LIC# SFWCOC*745
