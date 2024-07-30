# Web-Scraping

Scraped the data from wikepedia about List of Largest Companies in United Stated by revenue

### 1. Import Necessary Libraries
```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```
- **Description**: This step imports the necessary libraries for web scraping (`BeautifulSoup` and `requests`) and data manipulation (`pandas`).

### 2. Define the URL
```python
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
```
- **Description**: This step defines a variable `url` with the URL of the Wikipedia page listing the largest companies in the United States by revenue.

### 3. Fetch the Web Page
```python
page = requests.get(url)
```
- **Description**: This step sends an HTTP GET request to the specified URL and stores the response in the variable `page`.

### 4. Parse the HTML Content
```python
soup = BeautifulSoup(page.text, 'html.parser')
print(soup)
```
- **Description**: This step creates a `BeautifulSoup` object named `soup` by parsing the HTML content of the `page` response using the `html.parser`. It then prints the parsed HTML content.

### 5. Locate and Print the Table
```python
table = soup.find_all('table')[1]
print(table)
```
- **Description**: This step finds and prints the second table on the web page (as tables are indexed starting from 0). 

### 6. Extract and Print Table Headers
```python
titles = table.findAll('th')
print(titles)

titles_display = [i.text.strip() for i in titles]
titles_display
```
- **Description**: This step extracts all table headers (`<th>` elements), prints them, and then strips any extra whitespace from their text content, storing the cleaned header titles in `titles_display`.

### 7. Create DataFrame with Headers
```python
df = pd.DataFrame(columns=titles_display)
df
```
- **Description**: This step creates an empty `pandas` DataFrame with columns named after the cleaned table headers.

### 8. Extract and Print Table Rows
```python
row_data = table.find_all('tr')
print(row_data)
```
- **Description**: This step finds all table rows (`<tr>` elements) in the table and prints them.

### 9. Populate DataFrame with Table Data
```python
for i in row_data[1:]:
    col = i.find_all('td')
    row = [j.text.strip() for j in col]
    length = len(df)
    df.loc[length] = row
```
- **Description**: This step iterates through each row (excluding the header row), extracts the data from each cell (`<td>` elements), strips any extra whitespace, and adds the data to the DataFrame.

### 10. Save DataFrame to CSV
```python
df.to_csv(r'D:\Courses\Self\CS\Data Analyst\Scrappeddata.csv', index=False)
```
- **Description**: This step saves the populated DataFrame to a CSV file at the specified file path without including the DataFrame index.

This code effectively scrapes the specified table from the Wikipedia page, processes the data, stores it in a DataFrame, and then saves it as a CSV file for further analysis or use.
