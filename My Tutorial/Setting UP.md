# 🎥 Web Tutorial Script: Scrapy Crash Course with VS Code

---

## 🔴 INTRO

**Narration:**

> "Hey everyone! In this tutorial, I’ll show you how to go from zero to scraping with **Scrapy** using **VS Code**. We’ll install Scrapy, set up a project, write a few spiders, and export the data in different formats."

---

## 1️⃣ Installing Scrapy in a Virtual Environment

**Narration:**

> "Let’s start by setting up a virtual environment and installing Scrapy."

**Terminal Commands:**

```bash
# Create and activate a virtual environment
python -m venv scrapy_env

# Windows\scrapy_env\Scripts\activate
# macOS/Linux
source scrapy_env/bin/activate

# Install Scrapy
pip install scrapy
```

**VS Code Tip:**
Open VS Code inside the project folder:

```bash
code .
```

---

## 2️⃣ Creating a Scrapy Project

**Narration:**

> "Now let’s create our first Scrapy project."

**Terminal Commands:**

```bash
scrapy startproject quotes_scraper
cd quotes_scraper
```

**Project Structure:**

```
quotes_scraper/
├── scrapy.cfg
└── quotes_scraper/
    ├── __init__.py
    ├── items.py
    ├── middlewares.py
    ├── pipelines.py
    ├── settings.py
    └── spiders/
        └── __init__.py
```

---

## 3️⃣ Creating a Basic Spider

**Narration:**

> "Let’s create a spider that scrapes quotes from a demo site."

**File:** `quotes_scraper/spiders/quotes_spider.py`

```python
import scrapy

class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = ['http://quotes.toscrape.com']

    def parse(self, response):
        for quote in response.css("div.quote"):
            yield {
                'text': quote.css("span.text::text").get(),
                'author': quote.css("small.author::text").get(),
                'tags': quote.css("div.tags a.tag::text").getall(),
            }
```

---

## 4️⃣ Running the Spider

**Narration:**

> "Now, let’s run the spider and export the data to a JSON file."

**Terminal Command:**

```bash
scrapy crawl quotes -o quotes.json
```

**Result:** Show `quotes.json` in VS Code.

---

## 5️⃣ Following Links to Scrape Author Details

**Narration:**

> "Let’s enhance our spider to follow links and grab author bios."

**Update Spider:**

```python
def parse(self, response):
    for quote in response.css("div.quote"):
        author_url = quote.css("a::attr(href)").get()
        yield response.follow(author_url, self.parse_author)

def parse_author(self, response):
    yield {
        'name': response.css("h3.author-title::text").get().strip(),
        'birthdate': response.css("span.author-born-date::text").get(),
        'bio': response.css("div.author-description::text").get().strip()
    }
```

---

## 6️⃣ Using XPath Selectors (Alternate Example)

**Narration:**

> “You can also use XPath instead of CSS for scraping.”

**Example:**

```python
def parse(self, response):
    for quote in response.xpath("//div[@class='quote']"):
        yield {
            'text': quote.xpath("span[@class='text']/text()").get(),
            'author': quote.xpath("span/small[@class='author']/text()").get(),
            'tags': quote.xpath("div[@class='tags']/a[@class='tag']/text()").getall()
        }
```

---

## 7️⃣ Exporting Data to CSV

**Narration:**

> "You can also export to CSV or XML with one command."

**Command:**

```bash
scrapy crawl quotes -o quotes.csv
```

---

## 8️⃣ Using Scrapy Shell for Testing Selectors

**Narration:**

> "Use the Scrapy shell to test selectors interactively."

**Commands:**

```bash
scrapy shell http://quotes.toscrape.com
```

Then try:

```python
response.css("span.text::text").getall()
response.xpath("//span[@class='text']/text()").getall()
```

---

## 9️⃣ Bonus: Pagination

**Narration:**

> “Let’s scrape all pages by following the ‘Next’ button.”

**Update Spider:**

```python
def parse(self, response):
    for quote in response.css("div.quote"):
        yield {
            'text': quote.css("span.text::text").get(),
            'author': quote.css("small.author::text").get(),
            'tags': quote.css("div.tags a.tag::text").getall(),
        }

    next_page = response.css("li.next a::attr(href)").get()
    if next_page:
        yield response.follow(next_page, self.parse)
```

---

## 🔚 Wrap Up

**Narration:**

> “And that’s a quick crash course on Scrapy with VS Code! You learned how to install Scrapy, set up a project, write spiders, follow links, and export data in multiple formats.”

> “If this helped you, give it a like and subscribe. Check the description for the full code and extra resources.”
