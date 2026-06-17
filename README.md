# Bulk Image Dataset Collector

Scrape and download image datasets from any webpage to Google Drive.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/WhoisMonesh/Colab-Image-Dataset-Collector/blob/main/Colab-Image-Dataset-Collector.ipynb)

---

## Quick Start

1. **Open in Colab** (click badge above)
2. **Mount Drive** when prompted
3. **Paste your URL** in the `SOURCE_URL` field in section 3
4. **Run all cells**

Your images will appear in your Google Drive under `ImageDatasetCollector/`.

---

## Features

| Feature | Description |
|---|---|
| **Web Scraping** | Extracts all `<img>` tags from any public webpage |
| **Lazy-load Support** | Reads both `src` and `data-src` attributes |
| **Resolution Filter** | `MIN_WIDTH` / `MIN_HEIGHT` skip images that are too small |
| **Download Limit** | `MAX_IMAGES` caps total images downloaded |
| **HTML Progress** | Live progress bar showing count, percentage, dimensions |
| **Sync-safe** | Downloads locally first, then moves to Drive |
| **Keep-Alive** | JavaScript prevents Colab timeout during large scrapes |
| **Auto-Zip** | Multiple images are zipped with progress + download link |

---

## Where to Put the URL

In section **3. Configuration**, find this line and paste your URL:

```python
SOURCE_URL = 'https://unsplash.com/s/photos/nature'  # <-- paste your URL here
```

### Examples

| What to scrape | URL |
|---|---|
| Unsplash search | `https://unsplash.com/s/photos/nature` |
| Wallhaven search | `https://wallhaven.cc/search?q=landscape` |
| Any public page | `https://example.com/gallery` |
| Pexels photos | `https://pexels.com/search/mountains/` |

### How it works

The notebook fetches the HTML of your URL, parses all `<img>` elements, then downloads each image that meets your size requirements. Images are saved as `img_00001.jpg`, `img_00002.jpg`, etc.

**Limitations:**
- Works best with static HTML pages (images already in the source)
- JavaScript-rendered galleries may not be fully captured
- Some sites block automated requests — set a respectful `MAX_IMAGES` limit

---

## All Configuration Options

| Variable | Default | Description |
|---|---|---|
| `SAVE_PATH` | `/content/downloads/ImageDatasetCollector/` | Local temp directory |
| `DRIVE_PATH` | `/content/drive/My Drive/ImageDatasetCollector/` | Final Drive destination |
| `SOURCE_URL` | `'https://unsplash.com/s/photos/nature'` | Webpage URL to scrape images from |
| `MAX_IMAGES` | `500` | Maximum images to download |
| `MIN_WIDTH` | `200` | Minimum image width in pixels |
| `MIN_HEIGHT` | `200` | Minimum image height in pixels |
| `KEEP_ALIVE` | `True` | Prevent Colab timeout |

---

## Technical Details

- Uses `requests` + `BeautifulSoup` for HTML parsing
- `PIL` (Pillow) validates image dimensions before saving
- Respects min width/height by decoding the actual image, not relying on HTML attributes
- Downloads to `/content/downloads/` first, then `shutil.move` to Drive (avoids FUSE sync conflicts)
- Live progress via `IPython.display` HTML with `display_id`
- JavaScript keep-alive prevents Colab session timeout
- Automatic ZIP when multiple files are downloaded

---

## Fair Use & Legal Notice

This tool downloads publicly accessible images from webpages for **personal, non-commercial, educational use only**.

**You agree to:**
- Only scrape websites you have permission to access
- Respect `robots.txt` and website terms of service
- Use downloaded images in accordance with their original licenses (e.g. Creative Commons, public domain)
- Attribute sources where required by the license

**You may NOT use this tool to:**
- Scrape copyrighted images for commercial use
- Bypass paywalls, authentication, or access controls
- Mass-download content without respecting rate limits
- Violate any applicable copyright or data protection laws
- Re-upload or redistribute scraped content without permission

**Disclaimer:** The authors are not responsible for how you use this software. You assume all legal responsibility for the content you scrape and download. This tool is provided for educational purposes only. Website scraping may be subject to local laws and website terms of service — check before use.

---

## License

MIT
