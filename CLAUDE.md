# ParthSanepara Project Guide

This repository contains the GitHub profile README for [Parth Sanepara](https://github.com/ParthSanepara).

## Website: parthsanepara.in

The personal website is hosted separately. See SEO fixes below.

---

## SEO Issue Fix: Content-Signal Directive

### Problem
Google Search Console reports:
```
Line 29: Content-Signal: search=yes,ai-train=no
Unknown directive
```

### Understanding the Issue
The `Content-Signal` directive is a **Cloudflare-proposed robots.txt extension** for controlling AI crawler behavior. It's NOT a standard robots.txt directive, which is why Google reports it as "unknown."

**Important**: This warning does NOT negatively impact SEO. Google simply ignores directives it doesn't recognize.

### Fix Options

#### Option 1: Keep Content-Signal (Recommended)
If you want to control AI training while allowing search:
```robots.txt
User-Agent: *
Allow: /

# Cloudflare Content Signals Policy
# https://contentsignals.org/
Content-Signal: search=yes, ai-train=no, ai-input=no
```

The warning in Google Search Console can be safely ignored. Cloudflare and compliant crawlers will honor it.

#### Option 2: Remove Content-Signal
If you prefer no warnings in Google Search Console, remove the `Content-Signal` line entirely.

#### Option 3: Use Standard AI Crawler Blocks
Block specific AI crawlers using standard User-Agent rules:
```robots.txt
User-Agent: *
Allow: /

# Block AI training crawlers
User-Agent: GPTBot
Disallow: /

User-Agent: CCBot
Disallow: /

User-Agent: anthropic-ai
Disallow: /

User-Agent: Claude-Web
Disallow: /

User-Agent: Google-Extended
Disallow: /
```

---

## PageSpeed SEO Recommendations

Based on common PageSpeed Insights issues for mobile:

### Critical Fixes

1. **Largest Contentful Paint (LCP)**
   - Preload critical images: `<link rel="preload" as="image" href="hero.jpg">`
   - Use modern image formats (WebP, AVIF)
   - Implement lazy loading for below-fold images

2. **Cumulative Layout Shift (CLS)**
   - Always specify width/height on images
   - Reserve space for ads/embeds
   - Avoid inserting content above existing content

3. **First Input Delay / Interaction to Next Paint**
   - Defer non-critical JavaScript
   - Break up long tasks
   - Use `loading="lazy"` for iframes

### Essential Meta Tags
Ensure these are in your `<head>`:
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="description" content="Parth Sanepara - Embedded Systems Engineer, IoT Developer">
<meta name="robots" content="index, follow">
<link rel="canonical" href="https://parthsanepara.in/">

<!-- Open Graph -->
<meta property="og:title" content="Parth Sanepara">
<meta property="og:description" content="Embedded Systems Engineer & IoT Innovator">
<meta property="og:type" content="website">
<meta property="og:url" content="https://parthsanepara.in/">
<meta property="og:image" content="https://parthsanepara.in/og-image.jpg">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Parth Sanepara">
<meta name="twitter:description" content="Embedded Systems Engineer & IoT Innovator">
```

### Performance Checklist

- [ ] Enable Gzip/Brotli compression
- [ ] Set proper cache headers (1 year for static assets)
- [ ] Minify CSS/JS
- [ ] Use CDN for static assets
- [ ] Optimize images (compress, proper sizing)
- [ ] Implement critical CSS inlining
- [ ] Defer non-critical CSS/JS

### robots.txt Best Practice
```robots.txt
User-Agent: *
Allow: /
Sitemap: https://parthsanepara.in/sitemap.xml

# Optional: Block AI training while allowing search
Content-Signal: search=yes, ai-train=no, ai-input=no
```

---

## Resources

- [Content Signals Policy](https://contentsignals.org/)
- [PageSpeed Insights](https://pagespeed.web.dev/)
- [Google Search Console](https://search.google.com/search-console)
- [Web.dev SEO Guide](https://web.dev/learn/seo)
