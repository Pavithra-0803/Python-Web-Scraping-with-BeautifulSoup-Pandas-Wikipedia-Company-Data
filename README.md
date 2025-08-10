# Python Web Scraping with BeautifulSoup & Pandas: Wikipedia Company Data

## 📌 Project Overview
This project demonstrates how to scrape tabular data from a live web page using **BeautifulSoup** and process it with **pandas**.  
We extract the list of the largest companies in the United States by revenue from Wikipedia, clean and structure the data, and store it for further analysis.

## 🔍 Features
- Fetches HTML content from Wikipedia using `requests`
- Parses HTML with `BeautifulSoup` to locate and extract the target table
- Cleans and processes tabular data into a `pandas` DataFrame
- Saves the cleaned dataset for further analysis or visualization

## 🛠️ Technologies Used
- **Python 3**
- **BeautifulSoup4**
- **requests**
- **pandas**

## 📂 Data Source
Wikipedia – [List of largest companies in the United States by revenue](https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue)

## what we have done here
1️⃣ Importing Libraries
We begin by importing:

requests → to fetch the HTML page content.

BeautifulSoup (from bs4) → to parse and navigate HTML.

pandas → to store and process the data.

2️⃣ Fetching the Web Page
We define the Wikipedia URL containing the list of largest companies by revenue and use requests.get() to download the page content

url = "https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue"
page = requests.get(url)


3️⃣ Parsing HTML with BeautifulSoup
We parse the raw HTML text into a structured format that we can navigate easily

soup = BeautifulSoup(page.text, "html")

4️⃣ Locating the Target Table
We find the relevant table (wikitable sortable) containing the company data.

table = soup.find_all('table')[1]  # selecting the correct table

5️⃣ Extracting Table Headers
We retrieve all column names from the <th> elements inside the table

world_titles = table.find_all('th')
world_table_titles = [title.text.strip() for title in world_titles]

6️⃣ Creating an Empty DataFrame
We create a pandas DataFrame with these headers as columns.

df = pd.DataFrame(columns=world_table_titles)

7️⃣ Extracting Table Rows
We loop through each <tr> (table row), extract <td> cell values, clean them, and append them to the DataFrame.

column_data = table.find_all('tr')
for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = individual_row_data

8️⃣ Saving Data to CSV
Finally, we save the cleaned data into a CSV file for offline use.

df.to_csv(r'C:\Users\ASUS\Documents\web scraping\output\companies.csv', index=False)



## 👩‍💻 Author
**Pavithra B**  
📍 Bangalore, India  
📧 pavithraaz2002@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/pavithra-b-114358338)  
💻 [GitHub](https://github.com/Pavithra-0803)
