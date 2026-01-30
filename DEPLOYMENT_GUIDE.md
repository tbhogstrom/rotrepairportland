# Dry Rot Portland - Deployment Guide

## Site Overview

- **Domain:** dryrotportland.com
- **Business:** SFW Construction
- **Oregon License:** OR CCB# 166405
- **Washington License:** WA LIC# SFWCOC*745
- **Phone:** (503) 885-0236
- **Address:** 2552 NW Vaughn St., Portland, OR 97210

## File Structure

```
output/
├── index.html                    # Homepage
├── home.html                     # Alternate home page
├── blog.html                     # Blog listing
├── contact-us-2.html             # Contact page
├── free-rot-repair-estimate.html # Lead capture form
├── portland-flat-roof-repairs.html  # Flat roof service page
├── dry-rot-repair-cost-portland.html # Cost/pricing page
├── permanent-rot-repair-solution.html
├── the-hidden-costs-of-dry-rot.html
├── the-lifecycle-of-dry-rot.html
├── detecting-and-managing-rot-in-your-home.html
├── how-to-identify-dry-rot-on-your-home.html
├── why-do-your-windows-leak-when-it-rains.html
├── service-areas/               # 39 location pages
│   ├── ne-portland.html
│   ├── se-portland.html
│   ├── beaverton.html
│   └── ... (36 more)
└── service-areas-sitemap.xml    # Sitemap for service areas
```

## Pre-Deployment Checklist

### DNS & Hosting
- [ ] Domain registered: dryrotportland.com
- [ ] DNS configured to hosting server
- [ ] SSL certificate installed (Let's Encrypt or similar)
- [ ] Hosting environment ready (WordPress or static)

### Content Verification
- [ ] All Seattle references replaced with Portland
- [ ] Phone number: (503) 885-0236
- [ ] Address: 2552 NW Vaughn St., Portland, OR 97210
- [ ] Oregon License: OR CCB# 166405
- [ ] Washington License: WA LIC# SFWCOC*745
- [ ] Business name: SFW Construction
- [ ] Copyright: ©Copyright 2026 SFW Construction

### Forms & Tracking
- [ ] Contact form submissions routing to correct email
- [ ] Google Analytics property created and tracking code added
- [ ] Google Search Console verified
- [ ] Google Business Profile created/claimed

## Deployment Options

### Option 1: WordPress Installation (Recommended)

1. **Install fresh WordPress** on your hosting
2. **Import the Genesis theme** (Monochrome Pro child theme)
3. **Create pages** matching the content structure
4. **Import content** from HTML files into WordPress pages/posts
5. **Configure Yoast SEO** plugin
6. **Set up NitroPack** for performance optimization

### Option 2: Static HTML Hosting

1. Upload all HTML files to hosting
2. Configure server for clean URLs
3. Set up redirects as needed
4. Add SSL certificate

## Post-Deployment Tasks

### SEO Setup
1. Submit sitemap to Google Search Console
2. Submit sitemap to Bing Webmaster Tools
3. Verify all pages are indexed
4. Set up Google Business Profile listing

### Monitoring
1. Set up uptime monitoring (UptimeRobot, Pingdom)
2. Configure backup schedule
3. Set up security monitoring

### Content Differentiation
To avoid duplicate content issues:
1. Rewrite introduction paragraphs with unique content
2. Add Portland-specific testimonials
3. Include local project photos
4. Reference Portland-specific regulations and building codes

## Image Assets to Replace

The following images reference Seattle and should be replaced with Portland-branded versions:

- Logo (logo-rot-repair-portland.png)
- Service area map
- Project photos with Seattle landmarks
- Team/location photos

## Important URLs

| Page | URL |
|------|-----|
| Homepage | https://dryrotportland.com/ |
| Free Estimate | https://dryrotportland.com/free-rot-repair-estimate/ |
| Blog | https://dryrotportland.com/blog/ |
| Contact | https://dryrotportland.com/contact-us-2/ |
| Flat Roof | https://dryrotportland.com/portland-flat-roof-repairs/ |
| Cost Guide | https://dryrotportland.com/dry-rot-repair-cost-portland/ |

## Support

For questions about this deployment, refer to the transformation scripts in the build directory.
