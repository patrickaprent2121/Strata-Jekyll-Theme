---
layout: post
title: HW08 - Cleaning the “Dispatch”
date: 2019-07-07T14:37:44.000Z
categories: update
---

In a first step a), the scraped xml files of all “Dispatch” issues should be cleaned up from all the xml tagging, and saved as clean/pure text files. The second task b) was to create clean copies of all articles from the issues of the “Dispatch”.
For both tasks a python script was needed.

a) Cleaned issues of the “Dispatch” 
```
# importing python libraries
import re
import os

# setting paths to source and target folder
sourceFolder = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/08_/HW08/Download_Dispatch_copy/"
newFolder = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/08_/HW08/Target_Folder/"

# method listdir() returning a list containing the names of the entries in the directory given by path
listOfFiles = os.listdir(sourceFolder)

# for-loop iterating over list of all files
for f in listOfFiles:
# open(close) file via with statement
  with open(sourceFolder + f, "r", encoding="utf8") as f1:
      # read data
      data = f1.read()
      # removes markup from each file
      text = re.sub("<[^<]+>","", data)
      # rename file and folder
      newFile =  newFolder + f + "_modified.xml"

      with open(newFile, "w", encoding="utf8") as f9:
          # write text
          f9.write(text)
```
<img src="/images/fulls/008-2.jpg" class="fit image"> 


b) Cleaned articles of the “Dispatch” 

```
import re 
import os

source = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/08_/HW08/Download_Dispatch_copy/"
newFolder = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/08_/HW08/Tagret_Folder_b2/"

lof = os.listdir(source)
counter = 0 # general counter to keep track of the progress

for f in lof:
    if f.startswith("dltext"): # startswith string method, fileName test
        # open(close) file via with statement   
        with open(source + f, "r", encoding="utf8") as f1:
            text = f1.read()

            # regex search function, try to find the date, “group(1)” returns first parenthesized subgroup
            date = re.search(r'<date value="([\d-]+)"', text).group(1)

            # splitting the issue into articles/items
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
                    

	        # removes markup from each file
                text = re.sub("<[^<]+>", "", s)
                text = re.sub(" +\n|\n +", "\n", text)
                text = re.sub("\n+", ";;; ", text)

                # generating necessary bits 
                fName = date+"_"+unitType+"_"+str(c)

                itemID = "#ID: " + date+"_"+unitType+"_"+str(c)
                dateVar   = "#DATE: " + date
                unitType = "#TYPE: " + unitType
                header = "#HEADER: " #+ header
                text = "#TEXT: " + text

                # creating a text variable
                var = "\n".join([itemID,dateVar,unitType,header,text])
                #input(var)

                # saving
                with open(newFolder+fName+".txt", "w", encoding="utf8") as f9:
                    f9.write(var)

        # count processed issues and print progress counter at every 100        
        counter += 1
        if counter % 100 == 0:
            print(counter)
```

