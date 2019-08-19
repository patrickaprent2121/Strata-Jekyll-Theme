---
layout: post
title: HW07 - Scraping the “Dispatch”
date: 2019-08-18T14:37:44.000Z
categories: update
---


# Webscraping with wget

Webscraping with wget allows the automatic download of huge amounts of web content.

There are different approaches and therefore commands and parameters:

'''
wget link
wget -i file_with_links.txt
wget -i links.txt -P ./folderYouWantToSaveTo/ -nc
'''

# Download issues of “Richmond Times Dispatch” (Years 1860–1865)

The issues are available as xml files each. 
http://www.perseus.tufts.edu/hopper/collection?collection=Perseus:collection:RichTimes

To download all issues/articles from the Richmond Dispatch from 1860–1865, it was necessary to create a list with all links to the xml files - and therefore find a pattern of how all files are named and stored/linked.

Looking at the html source code of the main page linking to all articles it was possible to automatically aggregate a list with the IDs of every single article.
(in firefox) view-source:http://www.perseus.tufts.edu/hopper/collection?collection=Perseus:collection:RichTimes
<img src="/images/fulls/007-2.jpg" class="fit image"> 


Therefore the source code was opened in Sublime Text. 
Article 1 therein:
'''
<a href="text?doc=Perseus%3atext%3a2006.05.0001"			
<a href="search?doc=Perseus%3atext%3a2006.05.0001"
'''

Using regular expressions (text\?doc[^"]+) the strings identifying every single article were selected and copied to a new list. 

<img src="/images/fulls/007-3.jpg" class="fit image"> 


Before the strings, another part was added automatically to complete the download-URLs of every single article in the list:
'''
find: 
text?doc=Perseus%3atext%3a2006.05.
replace with:
http://www.perseus.tufts.edu/hopper/dltext?doc=Perseus%3Atext%3A2006.05.
'''

From this list all files were downloaded via wget, resulting in 1.348 articles.

