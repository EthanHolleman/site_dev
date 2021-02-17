---
title: "Scraping leafly.com cannabis strain data"
date: 2021-02-16
tags: ['programming', 'blogs', 'Python', 'R']
draft: false
---

Recently I was asked by a friend if they knew about any databases that classified
cannabis strains by symptoms people tend to use them to relieve. I didn't
know of the existence of any but had heard about [leafly.com](https://www.leafly.com/)
which catalogues user reviews of various cannabis strains and compiles data on
their characteristics. 

I thought this could be a good place for them to start and so I started looking
into what it would take to make a webscrapper to pull down all the data leafly
has complied on hundreds on cannabis strains.

It turns out it didn't take that much.

First, you can browse strains by going to the strains url at `https://www.leafly.com/strains`.
Conveniently, you can iterate through pages by just adding `?page=n` where
`n` is whatever page you want. 

I started looking through the html of these pages originally to find a way to
pull out urls that would lead to each individual strain's page but leafly
(conveniently for me) provides basically all the information it has on the strains
listed on a specific page in a nicely formatted json string in a script at the
bottom of the page.

I was using the `BeautifulSoup` package and so after getting the page content
with `requests` all it took was

```python
json_script = str(soup.find_all('script', id='__NEXT_DATA__'))
clean_json = re.sub('<.*?>', '', json_script)
json.loads(clean_json).pop() 
```

to extract, clean and load the json into a dictionary. I did this for all pages
and collected [167 json files](https://github.com/EthanHolleman/leafly_scraper/blob/main/json_data.tar.xz).

I then threw together a [quick python script](https://github.com/EthanHolleman/leafly_scraper/blob/main/Python/extract_terps_from_json.py) 
to pull out basic attributes about
each strain from the json file collection including metrics on the terpene 
content of each strain and the feelings strains tend to create for users,
collectively called "effect measurements".
These were both expressed as floats but I am not sure what the units could be
for either if there are any.

I wanted to see if I could use classify the phenotype of each strain (sativa, 
indicia or hybrid) based on the various terpene and / or effect measurements
in a way that was at least better than a random guess.

I choose to go with a random forest model using the `randomForest` library in
R since there are three possible classifications. The variable importance 
plots generated from the `varImpPlot` function after training the models on their
respective training sets is below.

![](/posts/images/effect_terp.png)

I then tested each model's predictive ability by using the models to predict on
the validation set and creating a confusion matrix for each model.

Observed (validation data) are the rows and predictions are columns.

**Terpene confusion matrix**

|        | Hybrid | Indica | Sativa |
|--------|--------|--------|--------|
| Hybrid | 696    | 32     | 3      |
| Indica | 218    | 11     | 0      |
| Sativa | 142    | 0      | 3      |

Using terpenes as the explanatory variables was worse then guessing and basically
just thought everything was a hybrid.

**Effect measurement confusion matrix**

|        | Hybrid | Indica | Sativa |
|--------|--------|--------|--------|
| Hybrid | 826    | 84     | 40     |
| Indica | 172    | 210    | 1      |
| Sativa | 161    | 1      | 92     |

Neither model did great, and there seems to be a preference for hybrids. This
may be because hybrids were the most prevalent phenotype in the leafly database.
Either way, fun little exercise that traversed web-scrapping, Python and R. 

If you would like to play around with the processed data (csv) you can download
it [at this link](https://github.com/EthanHolleman/leafly_scraper/blob/main/strains.tar.xz).






