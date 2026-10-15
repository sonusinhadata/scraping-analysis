# 📚 Book Scraping & Analysis
An end-to-end data analyst project: scrape **1,000 books** from [books.toscrape.com](https://books.toscrape.com), clean the raw data, and analyze pricing and rating patterns with Python.

## 🎯 Objective
To practice the full data pipeline (**Collect → Clean → Analyze → Visualize → Insights**) and answer one main question:

> **Do higher-rated books cost more?**
## 🛠️ Tools Used
Python · Requests · BeautifulSoup · Pandas · Matplotlib · Seaborn · Jupyter Notebook

## 🔄 Project Workflow
### 1. Data Collection (Web Scraping)
- Scraped all **50 pages** of the catalogue using `requests` and `BeautifulSoup`.
- Extracted five fields per book: title, price, star rating, availability, and link.
- Added a 1-second delay between requests to avoid overloading the server.
- Result: **1,000 rows** saved to `data/raw/books_raw.csv`.

### 2. Data Cleaning
| Problem found | Fix applied |
|---|---|
| `price` was stored as text with currency symbols (e.g. `Â£51.77`, an encoding issue) | Removed the symbols and converted the column to `float` |
| `availability` was a text sentence | Converted it to a boolean `in_stock` column |
| Possible duplicates | Checked and removed duplicates (**0** found) |
| Missing values | Checked every column (**0** found) |

The raw file was left untouched; the cleaned version was saved to `data/cleaned/books_cleaned.csv`.

### 3. Analysis & Visualization
Explored the price distribution, rating distribution, the relationship between price and rating, outliers (IQR method), and stock availability.

## 📊 Key Insights
### 1. Prices are spread evenly across a wide range
Book prices range from **£10.00 to £59.99**, with a mean of **£35.07** and a median of **£35.98**. Because the mean and median are close, the distribution is balanced rather than skewed toward cheap or expensive books. The standard deviation of about £14.45 shows that prices vary widely, so there is no single "typical" price point.

![Price Distribution](images/price_distribution.png)
### 2. Most books are not rated highly
Only **37.5%** of books are rated 4 or 5 stars, which means the majority (62.5%) sit at 3 stars or below. Ratings are not concentrated at the top, so a high rating is less common than a low or middle one.

![Rating Counts](images/rating_counts.png)
### 3. Price and rating are essentially unrelated
The average price is almost identical across all rating levels:

| Rating | Average Price |
|:---:|:---:|
| 1 ⭐ | £34.56 |
| 2 ⭐ | £34.81 |
| 3 ⭐ | £34.69 |
| 4 ⭐ | £36.09 |
| 5 ⭐ | £35.37 |

The correlation between rating and price is just **0.028**, which is very close to zero. A 5-star book costs about the same as a 1-star book (a difference of under £1 on average). **Answer to the main question: no, higher-rated books do not cost more.** Price is not a signal of quality in this dataset.

![Price by Rating](images/price_by_rating.png)
### 4. There are no price outliers
Using the IQR method, the outlier boundaries were below -£15.92 or above £85.48. Since the cheapest book is £10 and the most expensive is £59.99, **zero outliers** were found. Prices are consistent, with no suspicious or extreme values that would distort the analysis.

### 5. Every book is in stock
**100%** of the 1,000 books are marked "In stock", so availability could not be used to separate or compare books. A column with no variation carries no analytical value here.

## ⚠️ Limitations
- The site is a practice website with simulated data, so the patterns (especially the lack of correlation) may not reflect a real bookstore.
- Correlation measures only linear relationships and does not prove causation.
- Book categories were not collected, so category-level analysis was not possible.

## 🚀 How to Run
```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
pip install -r requirements.txt
jupyter notebook
```

Open the notebook and run all cells from top to bottom (**Kernel → Restart & Run All**). The scraping cell takes about a minute and creates the `data/` and `images/` folders automatically.
## 📁 Project Structure
```
├── data/
│   ├── raw/books_raw.csv
│   └── cleaned/books_cleaned.csv
├── images/
│   ├── price_distribution.png
│   ├── rating_counts.png
│   └── price_by_rating.png
├── webscrapping.ipynb
├── requirements.txt
└── README.md
```

## 🔮 Future Improvements

- Scrape each book's detail page to add **category** and analyze by genre
- Load the data into **SQLite** and answer the same questions using SQL
- Build a **Power BI / Tableau** dashboard
- Add price buckets (Budget / Mid / Premium) and compare ratings across them
- Schedule the scraper to track price changes over time

## ⚖️ Disclaimer

Data was scraped from books.toscrape.com, a site created specifically for scraping practice. Requests were rate-limited out of courtesy to the server.

---

⭐ If you found this useful, feel free to star the repo. I'm documenting my data analyst learning journey on LinkedIn: **(https://www.linkedin.com/in/sonusinha-dataanalyst/?isSelfProfile=true)**
