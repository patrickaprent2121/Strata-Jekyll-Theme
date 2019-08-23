---
layout: post
title: HW10 - Text to Map
date: 2019-08-21T14:37:44.000Z
categories: update
---

```
# importing python libraries
import re, os

# path to source folder
source = "/Users/patrickaprent/Google_Drive/UNI/KU-Methodenkurs-DH_2019/10_/TGN_Gazetteer/tgn_xml_0519/"

# def function with parameter "source"
def generateTGNdata(source):

    # list containing the names of the files in the directory 
    lof = os.listdir(source)

    # creating lists for the collected tgn places and corresponding coordinates, and a NA list
    tgnList = []
    tgnListNA = []
    count = 0

    # for-loop, looping through lof
    for f in lof:
        if f.startswith("TGN"): # fileName test and print filename
            print(f)
            # opening(closing) file
            with open(source+f, "r", encoding="utf8") as f1:
                data = f1.read() # reading data
                # save data to a list and split at every "Subject" tag
                data = re.split("</Subject>", data)
                # looping created subject list
                for d in data:
                    d = re.sub("\n +", "", d) # regex replacement function for cleaning for d in data
                    #print(d)

                    if "Subject_ID" in d:
                        # SUBJECT: getting tgn ID taking the definite Subject ID number
                        placeID = re.search(r"Subject_ID=\"(\d+)\"", d).group(1)
                        #print(placeID)

                        # NAME OF THE PLACE: getting placeName
                        placeName = re.search(r"<Term_Text>([^<]+)</Term_Text>", d).group(1)
                        #print(placeName)


                        # THE COORDINATES
                        if "<Coordinates>" in d:
                            # first, we search for the Latitude part and store it to latGr
                            latGr = re.search(r"<Latitude>(.*)</Latitude>", d).group(1)

                            # Longitude and Latitude in decimals are unfortunately not really precise in the tgn files  
                            # therefore within latGr we're getting degrees, minutes and seconds, and recalculate the decimal
                            degrees = re.search(r"<Degrees>(.*)</Degrees>", latGr).group(1)
                            minutes = re.search(r"<Minutes>(.*)</Minutes>", latGr).group(1)
                            seconds = re.search(r"<Seconds>(.*)</Seconds>", latGr).group(1)
                            decimal_lat = re.search(r"<Decimal>(.*)</Decimal>", latGr).group(1) 

                            # Calculating lat as decimal: 
                            # "try block" testing if there are coordinates at all. Otherwise giving out an error exception and "NA"
                            try:
                                lat = int(degrees) + (float(minutes) * 1/60) + (float(seconds) * 1/60 * 1/60)
                                lat = str(lat) # lat transformed to string

                                decimal_lat = str(decimal_lat) # decimal_lat also as string..

                                # ..and checking if there is a minus (for direction West/South), if so, adding that to variable "lat"
                                if "-" in decimal_lat: 
                                    lat = "-"+lat 
                            except ValueError: # error exception returning str "NA" when there are no coordinates
                                lat = "NA"

                            # the same for Longitude
                            lonGr = re.search(r"<Longitude>(.*)</Longitude>", d).group(1)

                            degrees = re.search(r"<Degrees>(.*)</Degrees>", lonGr).group(1)
                            minutes = re.search(r"<Minutes>(.*)</Minutes>", lonGr).group(1)
                            seconds = re.search(r"<Seconds>(.*)</Seconds>", lonGr).group(1)
                            decimal_lon = re.search(r"<Decimal>(.*)</Decimal>", lonGr).group(1)
                            

                            try:
                                lon = int(degrees) + (float(minutes) * 1/60) + (float(seconds) * 1/60 * 1/60)
                                lon = str(lon)

                                decimal_lon = str(decimal_lon)

                                if "-" in decimal_lon: 
                                    lon = "-"+lon 
                            except ValueError: 
                                lon = "NA"

                        # if there are no coordinates at all return "NA"
                        else:
                            lat = "NA"
                            lon = "NA"

                        # making a list appending placeID, placeName, lat, lon; separated by a tab
                        tgnList.append("\t".join([placeID, placeName, lat, lon]))
                    
                        #print(lat)
                        #print(lon)

                        # making list for no coordinates places with "NA"
                        if lat == "NA" or lon == "NA":
                            #print("\t"+ "; ".join([placeID, placeName, lat, lon]))
                            tgnListNA.append("\t".join([placeID, placeName, lat, lon]))

    # header for tsv file, tab-separated
    header = "tgnID\tplacename\tlat\tlon\n"

    # joining everything (tgnList + header) and writing/saving it as a tsv file to target location
    with open("21-08_tgn_data_light.tsv", "w", encoding="utf8") as f9a:
         f9a.write(header+"\n".join(tgnList))

    # same for the "tgnListNA"
    with open("21-08_tgn_data_light_NA.tsv", "w", encoding="utf8") as f9b:
         f9b.write(header+"\n".join(tgnListNA))

    # printing summary of the process
    print("TGN has %d items" % len(tgnList))

# call function with source
generateTGNdata(source)

# TGN has 2505153 items

```

<img src="/images/fulls/010a.jpg" class="fit image">
