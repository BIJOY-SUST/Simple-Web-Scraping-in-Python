### What is web scraping?
Web-Scraping A collection of small programs that extract data from a website and packages it to be useful with the use of BeautifulSoup, a Python package for parsing HTML and XML documents. Once you retrieve the raw HTML of a site, you can start to select and extract with BeautifulSoup, which parses raw HTML strings and produces an object that mirrors HTML documents' structure.

#### Q: Scrape the data from https://en.wikipedia.org/wiki/List_of_Game_of_Thrones_episodes and make a table with all the episodes. Do EDA on the data and tell a story.
#### Sol: Follow these steps to solve this question.

  `Let us import the required libraries-`
   ```python      
           import requests
           from bs4 import BeautifulSoup
           from IPython.display import HTML
   ```
   
  `Get the url-`
   ```python      
           url = "https://en.wikipedia.org/wiki/List_of_Game_of_Thrones_episodes"
   ```
   
  `Connecting to the website-`
   ```python      
           response = requests.get(url)
   ```
   
  `Create a BeautifulSoup object for parsing-`
   ```python      
           soup = BeautifulSoup(response.text, 'html5lib')
   ```
   
  `Extracting the required elements-`
   ```python      
           tables = soup.find_all('table',{'class':'wikitable plainrowheaders wikiepisodetable'})
           del tables[-1]
           season_list = {}
           ind = 0
           no_overall = 0
           for table in tables:
             no_overall+=1
             for row in table:
               row_data = row.find_all('tr',{'class':'vevent'})
               for single_row in row_data:
                 all_columns = single_row.find_all('td');
                 no_in_season = all_columns[0].text
                 title = all_columns[1].text
                 title = title[1:-1]
                 directed_by = all_columns[2].text
                 written_by = all_columns[3].text
                 original_air_date = all_columns[4].text
                 new_original_air_date = ""
                 for ch in original_air_date:
                   if ch=='(':
                     break;
                   else :
                     new_original_air_date+=ch;
                 new_original_air_date[:-1]
                 viewers = all_columns[5].text
                 new_viewers = ""
                 for ch in viewers:
                   if ch=='[':
                     break;
                   else :
                     new_viewers+=ch;
                 new_viewers[:-1]
                 ind+=1
                 season_list[ind] = [ind,no_overall, no_in_season, title, directed_by, written_by, new_original_air_date, new_viewers] 
   ```
   
  `Save it to a CSV file-`
   ```python      
           all_seasons.to_csv('content'/'drive'/'My Drive'/'Colab Notebooks'/'game_of_thrones.csv');
   ```
