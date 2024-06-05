
# Scraping Wisdom: Unveiling Inspiring Quotes from the Web

Description:

Unlock the treasure trove of wisdom scattered across the web with our web scraping project! Dive into a journey through the digital realm of quotes, where each page reveals new insights and inspiration. From renowned authors to thought-provoking tags, our project meticulously collects and organizes this valuable data, offering you a curated collection of quotes to uplift and motivate. Join us as we explore the realms of literature, philosophy, and beyond, one page at a time.



## Acknowledgements

 We extend our gratitude to the creators and maintainers of the following tools and resources, which were instrumental in the development of this web scraping project:

- Beautiful Soup: A Python library for pulling data out of HTML and XML files. Its simplicity and flexibility made parsing HTML content a breeze.

- Requests: An elegant and simple HTTP library for Python, which allowed us to effortlessly send HTTP requests and retrieve webpage data.

- Pandas: A powerful data manipulation and analysis library for Python. It enabled us to efficiently process and organize the scraped data into structured DataFrames.

- Quotes to Scrape: Special thanks to the website quotes.toscrape.com for providing a rich source of inspiring quotes, which served as the foundation for our project.

We are grateful for the contributions of these tools and resources, which significantly enhanced the development process and enriched the outcome of our project.
 
## API Reference

#### Get all items
#### requests.get()

```http
GET /api/items
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `url	string` | `Required` | **Required**. URL of the website to scrape |

#### BeautifulSoup()

```http
GET /api/items/${id}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `html_content` | `string` | HTML content of the webpage |


#### find_all()

```http
GET /api/items/${id}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `name` | `str/regex` | **Required**.Tag name or regex pattern to match attrs	dict Optional attributes to filter elements |

  
#### DataFrame()

```http
GET /api/items/${id}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `data` | `list` | **Required**. Data to be stored in the DataFrame columns	list	Optional column names for the DataFrame |

#### to_csv()

```http
 GET /api/items/${id}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `path_or_buf` | `str/file` | **Required**. ath to save the CSV file index	bool Whether to include the DataFrame index in the CSV file |

#### add(num1, num2)

```http
 Takes two numbers and returns the sum.
```


## Appendix

#### Code Snippet for Scraping Quotes
```http

link = 'https://quotes.toscrape.com/'
res = requests.get(link)
soup = BeautifulSoup(res.text, 'html.parser')
quotes = []
authors = []
for quote in soup.find_all('span', class_='text'):
    quotes.append(quote.text[1:-1])  # Append the quote text
for i in soup.find_all('small', class_='author'):
    authors.append(i.text)  # Append the author's name
data = []
for sp in soup.find_all('div', class_='quote'):
    quote = sp.find('span', class_='text').text[1:-1]  # Extract quote text
    author = sp.find('small', class_='author').text  # Extract author's name
    details = sp.find('a').get('href')  # Extract details link
    tags = [tag.text for tag in sp.find_all('a', class_='tag')]  # Extract tags
    tags = ','.join(tags)  # Convert tags list to a comma-separated string
    data.append([quote, author, details, tags])  # Append data to the list
```

#### Code Snippet for Scraping Data from Multiple Pages

```http
multiple_pages_data = []
for page in range(1, 11):
    # Construct the URL for each page
    page_link = f"http://quotes.toscrape.com/page/{page}"
    # Send a request to the website
    res = requests.get(page_link)
    # Create a soup object to parse the HTML content
    soup = BeautifulSoup(res.text, 'html.parser')
    # Loop through all elements with the specified class and extract desired information
    for sp in soup.find_all('div', class_='quote'):
        quote = sp.find('span', class_='text').text[1:-1]  # Extract quote text
        author = sp.find('small', class_='author').text  # Extract author's name
        details = sp.find('a').get('href')  # Extract details link
        tags = [tag.text for tag in sp.find_all('a', class_='tag')]  # Extract tags
        tags = ','.join(tags)  # Convert tags list to a comma-separated string
        multiple_pages_data.append([quote, author, details, tags])  # Append data to the list
```

#### Data Processing and Saving

```http

df = pd.DataFrame(data, columns=['Quote', 'Author', 'Details', 'Tags'])
print("Scraped Data from Single Page:")
print(df)
df.to_csv('scraped_data.csv', index=False)
print("Scraped data saved to 'scraped_data.csv'.")
df_multiple_pages = pd.DataFrame(multiple_pages_data, columns=['Quote', 'Author', 'Details', 'Tags'])
print("\nScraped Data from Multiple Pages:")
print(df_multiple_pages)
df_multiple_pages.to_csv('scraped_data_multiple_pages.csv', index=False)

```
## Authors

- [Shubham Saxena](https://github.com/Shubham-Saxena-16)

## Badges

Add badges from somewhere like: [shields.io](https://shields.io/)

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)
[![AGPL License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)
![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)

## Deployment

To deploy this project run,follow these steps:

####1. Clone the Repository:

```bash
  git clone https://github.com/Shubham-Saxena-16/Web_scrapping.git
```
####2. Navigate to the Project Directory:

```bash
 cd Web_scrapping/WEB_SCRAPING
```

####3.Install Dependencies:

```bash
 pip install -r requirements.txt
```

####4. Run the Application:

```bash
 python main.py
```

####5. Access the Application:

- Once the application is running, open your web browser and go to http://localhost:5000 to access the application.

## FAQ

#### Question 1 : What is web scraping?

Answer 1 : Web scraping is the process of extracting data from websites. It involves retrieving and parsing HTML or other structured data from web pages to extract specific information.

#### Question 2 : Is web scraping legal?

Answer 2: Web scraping legality depends on various factors such as the website's terms of service, the method used for scraping, and the type of data being scraped. It's essential to review and comply with the website's terms of service and adhere to applicable laws and regulations.

#### Question 3 :What tools or libraries are used for web scraping in Python?

Answer 3: Popular Python libraries for web scraping include BeautifulSoup, Scrapy, Selenium, and Requests.

#### Question 4 :What are the common challenges in web scraping?

Answer 4: Common challenges in web scraping include handling dynamic content, dealing with anti-scraping measures like CAPTCHA or rate limiting, and maintaining scraping legality and ethics.

#### Question 5 :How can I prevent getting blocked while scraping websites?

Answer 5: To avoid getting blocked, you can implement techniques such as rotating IP addresses, using proxies, limiting request frequency, and respecting robots.txt rules.

#### Question 6 :What data formats can I export scraped data to?

Answer 6: Scraped data can be exported to various formats such as CSV (Comma-Separated Values), Excel, JSON (JavaScript Object Notation), or directly to a database like MySQL or MongoDB.


## Features

Here are some concise feature ideas for your web scraping project:
-User Interface (UI): Create a user-friendly interface for inputting URLs, specifying scraping parameters, and viewing results.

-Dynamic Content Handling: Support scraping of websites with dynamic content loaded via JavaScript.

-Customizable Scraping Rules: Allow users to define custom scraping rules or XPath expressions.

-Data Export Options: Provide options to export scraped data to CSV, Excel, JSON, or a database.

-Scheduled Scraping: Enable automated scraping at specified intervals with email notifications.

-Scraping Authentication: Support websites requiring authentication for access.

-Proxy Support: Integrate proxy support to avoid IP blocking or rate limiting.

-Error Handling and Logging: Implement robust error handling and logging for debugging.

-Performance Optimization: Optimize scraping performance with parallel processing, asynchronous requests, and caching.

-Documentation and Tutorials: Provide comprehensive documentation and tutorials for users.
## 🚀 About Me
I'm Shubham Saxena, a performance analyst specializing in web technologies and data analysis. With a background in computer science, I excel in optimizing systems and processes to enhance performance and efficiency. I'm passionate about leveraging data-driven insights to drive strategic decisions and improve outcomes. Let's connect on LinkedIn to explore potential collaborations!

