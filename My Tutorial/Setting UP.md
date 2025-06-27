# 🎥 Web Tutorial Script: Scrapy Crash Course with VS Code
## 🔴 INTRO
---
**Narration:**

> ***"Hey everyone! In this tutorial, I’ll show you how to go from zero to scraping with **Scrapy** using **VS Code**. We’ll install Scrapy, set up a project, write a few spiders, and export the data in different formats."***

---


## **What Is Scrapy**

> ***So what is Scrapy ?***  
>***Scrapy** is an **open-source web crawling and web scraping framework** written in **Python**. It's widely used for extracting structured data from websites, which makes it useful for things like:*
>
>* **Data mining**
>* **Price monitoring**
>* **Lead generation**
>* **Market research**
>* **News aggregation**



____
## 🔧 **Key Features of Scrapy**
> **So what are the key features of Scrapy ?**  
> Scrapy has many features, these include.
>* **Fast and asynchronous**: *(Asynchronous means not happening at the same time,)* Built on top of **Twisted**, an asynchronous networking framework, which allows high-performance scraping.  
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✅ **"Built on top of Twisted"**  
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*     *Twisted is a Python framework specifically designed for handling network communication (like HTTP requests).*    
>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*     *Saying Scrapy is "built on top of Twisted" means Scrapy uses Twisted as its core engine for handling web requests and responses.*
> 
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✅ "An asynchronous networking framework"      
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Asynchronous means Scrapy can send many requests at once without waiting for each one to finish before starting the next.    
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Instead of saying “send request → wait → process → repeat,” it says:    
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    * ***“send request → send another → send another → handle them all as they finish.”***    
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* This makes Scrapy very fast and efficient, especially when scraping hundreds or thousands of pages.
>   
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✅ "Which allows high-performance scraping"  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Because of Twisted’s asynchronous nature, Scrapy can scrape websites much faster than traditional scripts that wait for each response one at a time.  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* This is why Scrapy is used in large-scale scraping jobs — it's designed for speed and performance.  
>
>* **Selectors based on XPath or CSS**: Helps extract data from HTML or XML documents.
>* **Built-in support for following links**: Useful for crawling through pages automatically.
>* **Item pipelines**: Clean, validate, and store scraped data (e.g., to databases or files).  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* ✅ **What are Pipelines,Explanation:**  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*🧼 Clean    
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Once Scrapy gathers data, it may need some touch-up — removing whitespace, fixing encoding issues, or formatting dates. This is the "cleaning" stage.  
>
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* ✅ Validate  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*This step checks if the data is complete and correct. For example, if a field like price should always be a number, this step makes sure that’s true — and can discard or fix bad data.  
>
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*💾 Store  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    After cleaning and validating, the data is stored somewhere — like:  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    A CSV file  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    A JSON file  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    A SQL or NoSQL database  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    Or even sent to an API  
>  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*🧠 In Context of Scrapy:  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    Scrapy uses Item Pipelines to run all these steps after the spider extracts the data.  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    You define a pipeline in pipelines.py, and Scrapy runs each item through it in order.  
>
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*💡 Analogy:  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Think of your scraped data like raw vegetables from a garden.  
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Pipelines are your kitchen:  
>
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    🧼 You wash (clean) them  
>
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    ✅ You inspect (validate) them  
>
>    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*    🍱 You store (save) them in containers  
>
> 
>* **Middleware system**: Allows custom behavior for request/response handling.
>* **Shell and logging**: Useful for testing and debugging.


____


## 🏗 Basic Scrapy Workflow

1. **Create a Scrapy project**
2. **Define an item** (structure of the data you want)
3. **Write a spider** (crawler that sends requests and parses responses)
4. **Process items via pipelines**
5. **Store/export the data** (CSV, JSON, database, etc.)

## 1️⃣ Creating a Scrapy Project
2️⃣
Narration:

***"Now let’s create our first Scrapy project."***

**Terminal Commands:**

```python
scrapy startproject quotes_scraper
cd quotes_scraper
```

**Project Structure:**

```quotes_scraper/
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

## 🔍 What Is a Spider in Scrapy?

Narration:
> ***"Next up, let’s talk about one of the most important parts of Scrapy: the spider."***

## 🕷️ What Is a Spider?

### ***"A spider in Scrapy is a Python class that defines how to crawl a website and what data to extract. It’s like a blueprint for where to go and what to grab."***

Visual Aid: (Display a flow diagram of spider -> website -> extracted data)

"Each spider needs at least:

- **A name**

- **A list of URLs to start from**

- **A method to parse the downloaded content"**

## 🤖 A Spider Is Like...

### *"Think of it like a robot you program. You tell it:*

- **Where to begin**

- **How to find the data**

- **What to do with it"**

## 📖 Example: Basic Spider

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
## ✅ What Happens When It Runs?

"When you run this spider with the `scrapy crawl` command, Scrapy:

- **Starts at the URL you give it**

- **Downloads the HTML**

- **Calls the parse function with the response**

- **Collects and outputs whatever data your spider yields"**

## 1️⃣ Installing Scrapy in a Virtual Environment

Narration:
> ***"Let’s start by setting up a virtual environment and installing Scrapy."***

**Terminal Commands:**

```python
# Create and activate a virtual environment
python -m venv scrapy_env

# Windows\scrapy_env\Scripts\activate
# macOS/Linux
source scrapy_env/bin/activate

# Install Scrapy
pip install scrapy
```

**VS Code Tip:** Open VS Code inside the project folder:

```
code .
```



## 3️⃣ Creating a Basic Spider

Narration:

***"Let’s create a spider that scrapes quotes from a demo site."***

File: `quotes_scraper/spiders/quotes_spider.py`

```import scrapy

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
____


To run this spider:

```bash
scrapy crawl quotes -o quotes.json
```

____




## 1️⃣ Installing Scrapy in a Virtual Environment

**Narration:**

> "Let’s start by setting up a virtual environment and installing Scrapy."
> Here's how you can **explain what an environment is** and **why it's needed**, written for a beginner-friendly **tutorial script**:

---

## 🎓 What Is an Environment in Python,and Why It Matters?

**Narration:**

> "Before we dive into coding, let’s talk about something important — environments."

### ✅ What Is a Python Environment?

> "A Python environment is like a *workspace* for your code. It contains everything your project needs to run — including Python itself, and any libraries or tools your code depends on."

### 🧪 Think of it like:

> "Imagine you're baking. Each recipe might need different ingredients — some recipes need chocolate chips, some need cinnamon, and some need none at all. A **Python environment** is like having a separate pantry for each recipe so that ingredients don’t get mixed up or go bad."

---

## ❓ Why Do We Need Virtual Environments?

### 1. **Avoid Conflicts**

> "Different projects often need different versions of libraries. For example, one project might use Scrapy version 2.5, while another needs version 2.10. A virtual environment keeps these separate, so one project doesn’t break the other."

### 2. **Keep Things Organized**

> "All dependencies for a project are stored in one folder. That makes it easy to manage, share, and reproduce the setup — especially when you share your code with someone else."

### 3. **Safe Testing**

> "You can test new packages or code safely without affecting your main Python installation."

---

## 🛠 What Happens When You Create an Environment?

> "When you run this command:"

```bash
python -m venv myenv
```

> "Python creates a folder called `myenv` that contains a fresh copy of Python and a blank slate for installing packages."

---

## 🏁 Final Summary

> "So, a Python environment helps keep your projects clean, organized, and conflict-free. It’s a best practice to create a new environment for every project — especially when working with tools like Scrapy."

____

### **Narration:**

>"Let’s start by setting up a virtual environment and installing Scrapy."

## **Terminal Commands:**


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
