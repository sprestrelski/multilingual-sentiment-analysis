Data Collection
- [NewsNow API](https://rapidapi.com/rphrp1985/api/newsnow)
    - get by category and by location, only get 50 API calls
    - Countries: United States/US, Germany/DE, France/FR, China/CN, Indonesia/ID
    - Languages: English/en, German/de, French/fr, Chinese/zh-Hant, Indonesian/id

API Calls
- 5 of match country to the language + 4 of english news in other countries
    - United States - English
    - China - Chinese
    - China - English
    - France - French
    - France - English
    - Germany - German
    - Germany - English
    - Indonesia - Indonesian
    - Indonesia - English
- 5 calls per country/language pair ==> top news by category for WORLD, NATION, TECHNOLOGY, ENTERTAINMENT, HEALTH


- exploratory inspect a couple news outlets by hand on the topic in English (ie. Fox vs NYT)
- focus on one or two events, should be important world-wide (ie. companies or global politics)
    - look for event that connects two outlets or two nations 
        - UN international court, can look for specific day for different points of view
- look into huggingface news datasets rather than API, okay to look from historical perspective 
- should be able to compare between UK/US for news outlets


1. Rank average happiness of different news sources in different languages
    - [Happiness of News](https://hedonometer.org/showcase/nyt/) has word lists in different languages
    - Dataset of articles related to the topic
    - Lookup each word in the dataset and average (?) the happiness score, need to determine metric
    - Happiness metrics verified in diff languages since not a model, distill-BERT is predictive so maybe not accurate
    - Languages: german/korean/spanish/russian/english/chinese/arabic/portuguese/french/ukranian
2. Rank positivity/neutral/negativity of different news sources in different languages
    - [HuggingFace Distill-BERT multilingual model](https://huggingface.co/lxyuan/distilbert-base-multilingual-cased-sentiments-student)
    - Languages: en/ar/de/es/fr/ja/zh/id/hi/it/ms/pt



```
import requests

locations = ['us', 'de', 'fr', 'cn', 'id']
languages_news = ['en', 'de', 'fr', 'zh-Hant', 'id']
languages_happiness = ['en', 'de', 'fr', 'zh', 'id']
categories = ['WORLD', 'NATION', 'TECHNOLOGY', 'ENTERTAINMENT', 'HEALTH']

url = "https://newsnow.p.rapidapi.com/newsv2_top_news_cat"

payload = {
	"category": "TECHNOLOGY",
	"location": "",
	"language": "en",
	"page": 1
}
headers = {
	"content-type": "application/json",
	"X-RapidAPI-Key": "",
	"X-RapidAPI-Host": "newsnow.p.rapidapi.com"
}


# response = requests.post(url, json=payload, headers=headers)

# print(response.json())
```


Project Workflow

1. Download news dataset
2. Run language prediction model to figure out language
3. Run models to detect sentiment 
- English, German, Spanish, French
- Thai and Korean
4. Filter down to specific events (search text for mention of specific events) 

todo:
- pick specific events
- compare sentiment of analysis in different language
- compare sentiment of analysis of english and other language
- visualize the sentiments of news in different languages on a graph 


- events
    - world climate conference
    - covid 
    - sedan coup
    - french election

- for each event
    - which languages are covering it?
        - counts of language
    - does the sentiment differ per language? 
        - sentiment graph of language
