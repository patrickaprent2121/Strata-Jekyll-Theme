---
layout: post
title: HW09 - Restructuring the “Dispatch”
date: 2019-07-08T14:37:44.000Z
categories: update
---
This task was to reformat and restructure the Dispatch files and create one TSV-file (Tab-separated value) with the entire content. Each article should appear as a single record and include:

* date;
* type of an entry (articles, advertisements, notices, etc);
* header;
* the text of an entry.

It was done with this python script:
```
# importing necessary libraries
import re, os

# source and target folder
source = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/08_/HW08/Download_Dispatch_copy/"
target = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/09_/HW09/Target/"

# list containing the names of the entries in the directory 
lof = os.listdir(source)

# counter to keep track of the progress
counter = 0 

# creating list
ourCSV = []

# for loop through lof
for f in lof:
    if f.startswith("dltext"): # fileName test 
# open(close) file using UTF-8 encoding, save it to f1 variable    
        with open(source + f, "r", encoding="utf8") as f1:
            text = f1.read()

            # try to find the date via the xml tag
            date = re.search(r'<date value="([\d-]+)"', text).group(1)

            # splitting the issue into articles/items via the xml tag
            split = re.split("<div3 ", text)

            c = 0 # item counter
            for s in split[1:]:
                c += 1
                s = "<div3 " + s # a step to restore the integrity of items
                #input(s)

                # try to find a unitType
                try:
                    unitType = re.search(r'type="([^\"]+)"', s).group(1)
                except:
                    unitType = "noType"
                    print(s)

                # try to find a header using XML tags, and if there is no header print so.
                try:
                    header = re.search(r'<head>(.*)</head>', s).group(1)
                    header = re.sub("<[^<]+>", "", header)
                except:
                    header = "NO HEADER"
                    #print("No header found!")

		# some text cleaning via regular expressions
                text = re.sub("<[^<]+>", "", s)
                text = re.sub(" +\n|\n +", "\n", text)
                text = re.sub("\n+", ";;; ", text)

                # generating necessary bits 
                fName = date+"_"+unitType+"_"+str(c)

                itemID = date+"_"+unitType+"_"+str(c)
                dateVar   = date
                #unitType = unitType
                #header = header
                text = text.replace("\t", " ")

                # creating a text variable
                var = "\t".join([itemID,dateVar,unitType,header,text])
                #input(var)

                ourCSV.append(var)


        # count processed issues and print progress counter at every 100        
        counter += 1
        if counter % 100 == 0:
            print(counter)

# saving
with open("dispatch_as_TSV.csv", "w", encoding="utf8") as f9:
    f9.write("\n".join(ourCSV))
print(counter)

```
<img src="/images/fulls/009-b.jpg" class="fit image"> 
