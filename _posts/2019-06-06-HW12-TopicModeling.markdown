---
layout: post
title: HW12 - Topic Modeling
date: 2019-06-06T14:37:44.000Z
categories: update
---

The Task was topic modeling the “Dispatch” with a provided R-script and with the jupyter notebook. 

First, the script “modelled” 20 topics:

```
{'t00': 'mr, bill, committee, house, senate, resolution, confederate, states, '
        'congress, military',
 't01': 'court, charged, yesterday, mr, stealing, slave, case, john, mayor, '
        'arrested',
 't02': 'company, express, southern, soldiers, associations, jpriv, friends, '
        'richmond, quartermaster, wpriv',
 't03': 'richmond, slaves, oclock, city, river, daily, office, page, john, '
        'meeting',
 't04': 'york, army, general, th, rebel, gen, grant, washington, rebels, '
        'thousand',
 't05': 'general, th, tennessee, captured, cavalry, hundred, army, gen, '
        'prisoners, thousand',
 't06': 'treasury, bonds, notes, states, confederate, cent, secretary, '
        'department, exchange, certificates',
 't07': 'sale, th, street, oclock, co, house, city, auction, st, streets',
 't08': 'dispatch, confederate, states, navy, richmond, cents, district, '
        'office, week, charge',
 't09': 'th, oclock, friends, residence, funeral, attend, family, died, aged, '
        'take',
 't10': 'virginia, company, general, major, maryland, regiment, army, camp, '
        'colonel, war',
 't11': 'prisoners, yankee, fire, city, shot, yesterday, mr, night, captain, '
        'officers',
 't12': 'th, co, miss, va, capt, mrs, john, wm, lieut, col',
 't13': 'certificates, government, treasury, supplies, free, states, taxation, '
        'officers, secretary, indebtedness',
 't14': 'service, officers, officer, persons, enrolling, general, th, orders, '
        'duty, state',
 't15': 'reward, dollars, feet, richmond, negro, th, county, inches, black, '
        'hundred',
 't16': 'war, government, states, country, mr, peace, south, united, state, '
        'power',
 't17': 'enemy, gen, army, wounded, yesterday, general, line, miles, cavalry, '
        'night',
 't18': 'governor, commonwealth, county, smith, virginia, court, william, '
        'king, richmond, proclamation',
 't19': 'priv, prices, price, pounds, st, pound, bushel, horses, profits, hire'}
```
Most topics certainly make sense in the context of historical events and developments (Civil War, Richmond). Some, on the other hand, seem to be too generic or are just not really useful at first glance. 
“t15” - by all its cruelty from todays perspective - seemed to be quite concrete and straightforward contentwise, and (at that point still unaware that Robert K. Nelson is also featuring it heavily in his project “Mining the Dispatch”) I wanted to look deeper into this topic and texts. A huge amount of the Dispatch issues feature what Nelson describes as “fugitive slave advertisements”, where there are “rewards” of a certain amount of “dollars” offered for relevant tips or the return of fugitive slaves, who were then described by their outward appearance, the location they were last seen etc. 
Looking into the texts, it becomes apparent that certain words are used repeatably in always very similar structured articles. These patterns of word usage and structure are detected by the algorithms, and assigned relatively as topics to the articles. 

<img src="/images/fulls/12a.jpg" class="fit image"> 

<img src="/images/fulls/12b.jpg" class="fit image">

This, the possibility to automatically visualise long-term developments (represented via the topics) backed by (hugely) large samples, certainly are very useful tools and methods for historians that - when critically applied - allow new perspectives on certain research areas, especially the graphs visualising the (relative) appearance - the trend of a topic - compared to other topics and incisive historical events (as utilized in Nelsons work).
<br />
<br />
Comparing the models for 20, 30 and 40 topics, it is interesting to see that some remain consistant also with the assoziated keywords, while others get kind of unpicked. As an example for the former


 
