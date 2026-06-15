# yt-channel-harvester

> Automated YouTube channel metadata extraction using Selenium with headless Chrome, infinite-scroll handling, and structured CSV export.

---

## Overview

`yt-channel-harvester` is a Python-based web scraping pipeline that extracts video metadata from any public YouTube channel. It handles dynamic content loading via infinite scroll, parses view counts, and exports clean, analysis-ready CSV files with Arabic-safe encoding.

---

## File Architecture

```
yt-channel-harvester/
│
├── youtube_channel_pipeline.ipynb   # Main scraping & analysis notebook
│
└── output/
    └── <channel>_videos_<YYYYMMDD_HHMMSS>.csv   # Exported video metadata
```

---

## Notebook Structure

| § | Section | Description |
|---|---------|-------------|
| 1 | Dependencies | Install Selenium, webdriver-manager, Pandas |
| 2 | Imports & Logging | All modules + structured logger |
| 3 | Configuration | Channel URL, scroll params, output paths |
| 4 | Chrome Driver Factory | Headless Chrome with anti-detection hardening |
| 5 | Helper Utilities | Safe element access, view parser, scroll engine |
| 6 | YouTubeChannelScraper | OOP scraper class with context manager |
| 7 | Execution | Run the scraper |
| 8 | DataFrame Build | Type casting, cleaning, deduplication |
| 9 | Data Quality | dtypes, null counts, view statistics |
| 10 | Exploration | Top videos, upload frequency distribution |
| 11 | CSV Export | UTF-8-sig encoding for Arabic-safe Excel output |
| 12 | Verification | Reload and sanity-check the saved file |

---

## Tech Stack

| Layer | Library |
|-------|---------|
| Scraping | Selenium 4 |
| Driver management | webdriver-manager |
| Data processing | Pandas |
| Language | Python 3.9+ |

---

## Extracted Fields

| Field | Description |
|-------|-------------|
| `title` | Video title |
| `url` | Full video URL |
| `views` | View count (parsed integer) |
| `upload_date` | Upload date string |
| `duration` | Video duration |

---

## Quick Start

**1. Configure the target channel** — edit only the config cell (§ 3):

```python
CHANNEL_URL    = "https://www.youtube.com/@YourChannel/videos"
CHANNEL_HANDLE = "@YourChannel"
MAX_VIDEOS     = 0      # 0 = scrape all videos
```

**2. Run all cells** — the scraper will open a headless browser, scroll the full channel page, extract metadata, and save a CSV to `output/`.

**3. Find your output** at:
```
output/<channel>_videos_<timestamp>.csv
```

---

## Notes

- Pass `headless=False` to `build_driver()` to observe the browser live during development.
- The scraper masks `navigator.webdriver` to reduce bot detection.
- Output is encoded as `UTF-8-sig` for compatibility with Arabic text in Excel.

---

## Author

**Ali Essam** · [ali-essam2002](https://github.com/ali-essam2002)
