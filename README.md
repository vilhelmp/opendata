# Open Data
List of open data resources ordered by country and topic.  

Currently pretty much just TOML/markdown files with lists of resoures. 

Planning on organizing it a bit better when I have more, and also make it possible to get the WMS/WFS/API/etc urls directly to query more easily.   

View list for [Sweden](sweden.md),  [Denmark](denmark.md), and  [Global](global.md)

# Quick example of working with the data in Python:

Import necessary libraries
```
import toml
import pandas as pd
import requests
```

Load the file directly and parse the TOML into a Python dictionary.
```
data = toml.loads( requests.get("https://raw.githubusercontent.com/vilhelmp/opendata/main/sweden.toml").text)
data

{'sweden': {'disclaimer': 'Not all resources that the APIs provide are available unauthorized.',
  'collections': [{'name': 'Sveriges Dataportal',
    'tags': ['collection'],
    'url': 'https://www.dataportal.se'},
   {'name': 'INSPIRE',
    'tags': ['collection', 'europe', 
 ...  
```
The output was truncated for brevity. Now at the lowest level there are "TOML-tables", which are lists of dictionaries. 
As such they can be read into Pandas directly.

```
df = pd.DataFrame( data['sweden']['collections'])
print(df.to_markdown())


|    | name                | tags                                | url                                                                                    | comments                                            |
|---:|:--------------------|:------------------------------------|:---------------------------------------------------------------------------------------|:----------------------------------------------------|
|  0 | Sveriges Dataportal | ['collection']                      | https://www.dataportal.se                                                              | nan                                                 |
|  1 | INSPIRE             | ['collection', 'europe', 'inspire'] | https://inspire-geoportal.ec.europa.eu/results.html?country=se&view=details&theme=none | nan                                                 |
|  2 | data.europa.eu      | ['collection', 'europe']            | https://data.europa.eu/sv                                                              | nan                                                 |
|  3 | geodataportalen     | ['GIS', 'maps']                     | https://www.geodata.se/geodataportalen/                                                | nan                                                 |
|  4 | GeoNode Gallery     | ['GIS', 'maps', 'collection']       | https://geonode.org/gallery/                                                           | Mainly GeoNode CMS access to mostly global datasets |
|  5 | FreeGISData.org     | ['']                                | http://freegisdata.org/place/210829/                                                   | Incomplete but most seems to work at least.         |
```




