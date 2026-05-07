# 🕷️ Production Web Scraper

A reusable, plug-and-play web scraper built with Python. The scraper functions are already defined — users just need to configure the website link and HTML selectors to scrape any website and automatically save the data as CSV and JSON.

---

## 📌 What This Project Does

- Fetches HTML content from any website
- Extracts data using HTML tags and class selectors
- Supports **multi-page pagination** automatically
- Saves scraped data as both **CSV** and **JSON**
- Logs all activity and errors to `scraper.log`
- Adds delays between requests to avoid getting blocked

---

## 🗂️ Project Structure

```
Scrapper/
│
├── scraping.py        # Main scraper code
├── requirements.txt   # Python dependencies
├── .gitignore         # Files to exclude from GitHub
└── README.md          # Project documentation
```

---

## ⚙️ How It Works

The project has two main classes:

### `ScraperConfig` — Settings
| Parameter | Description |
|---|---|
| `base_url` | The website URL you want to scrape |
| `selectors` | HTML tags and classes to extract (e.g. `h3`, `p.price_color`) |
| `pagination` | Start page, end page, and URL format for multi-page scraping |
| `delay` | Seconds to wait between requests (default: 2) |

### `ProductionScraper` — Worker
| Parameter | Description |
|---|---|
| `config` | Takes the ScraperConfig settings |
| `headers` | Sends a browser identity to avoid bot detection |
| `results` | Collects all scraped data internally |

**Flow:**
```
ScraperConfig (your settings)
        ↓
ProductionScraper.scrape()
        ↓
fetch_page() → downloads raw HTML
        ↓
parse_page() → extracts data using selectors
        ↓
save_json() / save_csv() → exports results
```

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/your-username/Scrapper.git
cd Scrapper
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure your target website

Open `scraping.py` and update the config block at the bottom:

```python
config = ScraperConfig(
    base_url="https://your-website.com/",
    selectors={
        "titles": {"tag": "h3", "class": None},
        "prices": {"tag": "p", "class": "price_color"}
    },
    pagination={
        "start": 1,
        "end": 3,
        "url_format": "https://your-website.com/page-{}.html"
    },
    delay=2
)
```

### 4. Run the scraper
```bash
python scraping.py
```

### 5. Output
- `books.json` — scraped data in JSON format
- `books.csv` — scraped data in CSV format
- `scraper.log` — logs of all activity and errors

---

## 📦 Dependencies

```
requests
beautifulsoup4
pandas
tenacity
```

Install all with:
```bash
pip install -r requirements.txt
```

---

## 🌐 Example — Books to Scrape

The default config scrapes [books.toscrape.com](https://books.toscrape.com/) — a free website made for practicing scraping.

It extracts:
- Book **titles** from `<h3>` tags
- Book **prices** from `<p class="price_color">` tags
- Across **3 pages** using pagination

---

## ⚠️ Limitations

- Works only on **static HTML based websites**
- Does not support **JavaScript rendered pages** (e.g. Amazon, Flipkart, Twitter)
- Cannot scrape **login protected pages** without session/cookie handling
- Can be extended using **Selenium** or **Playwright** for dynamic websites

---

## 📝 Notes

- To scrape a different website, only change the `config` block — no other code needs to be modified
- Delay is set to 2 seconds by default to be respectful to servers
- All errors are logged in `scraper.log` for easy debugging

---

## 👤 Author

**Sakthivel**  
Feel free to fork, use, and improve this project!
