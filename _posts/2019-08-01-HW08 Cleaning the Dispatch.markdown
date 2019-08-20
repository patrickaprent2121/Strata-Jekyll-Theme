---
layout: post
title: HW08 - Cleaning the “Dispatch”
date: 2019-07-08T14:37:44.000Z
categories: update
---
# HW08 - Cleaning the “Dispatch”

In a first step a), the scraped xml files of all “Dispatch” issues should be cleaned up from all the xml tagging, and saved as clean/pure text files.

The second task b) was to create clean copies of all articles from the issues of the “Dispatch”.

For both tasks a python script was needed.

a)
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
