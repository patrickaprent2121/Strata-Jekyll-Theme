
# Webscraping with wget

Webscraping with wget allows the automatic download of huge amounts of web content.

There are different approaches and therefore commands and parameters:

```
wget link
wget -i file_with_links.txt
wget -i links.txt -P ./folderYouWantToSaveTo/ -nc
```

# Download issues of “Richmond Times Dispatch” (Years 1860–1865)

The issues are available as xml files each. 
http://www.perseus.tufts.edu/hopper/collection?collection=Perseus:collection:RichTimes

To download all issues/articles from the Richmond Dispatch from 1860–1865, it was necessary to create a list with all links to the xml files - and therefore find a pattern of how all files are named and stored/linked.

Looking at the html source code of the main page linking to all articles it was possible to automatically aggregate a list with the IDs of every single article.
(in firefox) view-source:http://www.perseus.tufts.edu/hopper/collection?collection=Perseus:collection:RichTimes
<img src="/images/fulls/007-2.jpg" class="fit image"> 

