# drug_scraper
Collate various pieces of prescription drug information found online. Aim is to pull a list of potential drugs from a given indication. 


## Get drug or treatment details
(https://bnf.nice.org.uk/drug/)  
(https://bnf.nice.org.uk/interaction/)  
(https://bnf.nice.org.uk/treatment-summary/)  
(https://bnf.nice.org.uk/drug/macrogol-3350.html)  


## XPath to get entry in list of drugs, treatment summaries, interactions
```
//div[contains(@class, "span11")]/*/li/a/@href
```


## XPath to get indications from drug page
//span[contains(@class,"indication")]/span[contains(@class,"indication")]

## Also need to get the BNF details from somewhere. Open prescribing have an API
(https://openprescribing.net/api/1.0/bnf_code/?q=mesna)  
(https://openprescribing.net/api/1.0/bnf_code/?q=metoclopramide%20hydrochloride)  
(https://openprescribing.net/api/1.0/bnf_code/?q=macrogol%203350)  


## First version of script

```python
import requests
from lxml import html

res = requests.get('https://bnf.nice.org.uk/drug/')
tree = html.fromstring(res.content)
urls = tree.xpath('//div[contains(@class, "span11")]/*//@href')
```

