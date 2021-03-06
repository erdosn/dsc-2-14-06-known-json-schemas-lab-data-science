
# Working with Known JSON Schemas - Lab

## Introduction
In this lab you'll practice working with json files whose schema you know beforehand.

### Objectives
YWBAT
* Give 2 or more examples of why a schema is important
    * To insert correct types
    * Schema provides an nice outline
    * Schema and is a good description of the file
    * Plan your feature engineering/ analysis
* Use the schema to enhance our code in python

## Objectives
You will be able to:
* Read JSON Documentation Schemas and translate into code
* Extract data from known json schemas
* Write data to predefined JSON schemas

## Reading a JSON Schema

Here's the JSON schema provided for a section of the NY Times API:
<img src="nytimes_movie_schema.png" width=500>

or a fully expanded view:

<img src="nytimes_movie_schema_detailed.png" width=500>

You can see this yourself here:
https://developer.nytimes.com/movie_reviews_v2.json#/Documentation/GET/critics/%7Bresource-type%7D.json

You can see that the master structure is a dictionary and has a key named 'response'. This is also a dictionary and has two keys: 'data' and 'meta'. As you continue to examine the schema hierarchy, you'll notice the vast majority in this case are dictionaries. 

## Loading the Data File

Start by importing the json file. The sample response from the api is stored in a file **ny_times_movies.json**


```python
#Your code here
import pandas as pd
import json
```


```python
string_dict = '''{"a": 1, "b":2}'''
```

## Loading Specific Data

Create a DataFrame of the major data container within the json file, listed under the 'results' heading in the schema above.


```python
#Your code here
# Read this in 'normally'
# load vs loads ? 
# loads -> strings (.txt)
# load -> .json file

# read this in 'safely'

with open("ny_times_movies.json") as f: # auto close your file
    movies_data = json.load(f)
    
with open("ny_times_response.json") as f:
    ny_response = json.load(f)
```


```python
for k, v in ny_response.items():
    print("{} is type {}".format(k, type(v)))
```

    status is type <class 'str'>
    copyright is type <class 'str'>
    response is type <class 'dict'>



```python
movies_data

# what to do first?
for k, v in movies_data.items():
    print(k)
    print(v)
    print("\n\n\n")
```

    status
    OK
    
    
    
    
    copyright
    Copyright (c) 2018 The New York Times Company. All Rights Reserved.
    
    
    
    
    has_more
    True
    
    
    
    
    num_results
    20
    
    
    
    
    results
    [{'display_title': 'Can You Ever Forgive Me', 'mpaa_rating': 'R', 'critics_pick': 1, 'byline': 'A.O. SCOTT', 'headline': 'Review: Melissa McCarthy Is Criminally Good in ‘Can You Ever Forgive Me?’', 'summary_short': 'Marielle Heller directs a true story of literary fraud, set amid the bookstores and gay bars of early ’90s Manhattan.', 'publication_date': '2018-10-16', 'opening_date': '2018-10-19', 'date_updated': '2018-10-17 02:44:23', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/16/movies/can-you-ever-forgive-me-review-melissa-mccarthy.html', 'suggested_link_text': 'Read the New York Times Review of Can You Ever Forgive Me'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/19/arts/19CANYOUEVER-1/19CANYOUEVER-1-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Charm City', 'mpaa_rating': '', 'critics_pick': 1, 'byline': 'BEN KENIGSBERG', 'headline': 'Review: ‘Charm City’ Vividly Captures the Streets of Baltimore', 'summary_short': 'Marilyn Ness’s documentary is dedicated to the memory of the more than 1,000 people said to be killed in Baltimore during the film’s making.', 'publication_date': '2018-10-16', 'opening_date': '2018-04-22', 'date_updated': '2018-10-16 11:04:03', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/16/movies/charm-city-review-baltimore.html', 'suggested_link_text': 'Read the New York Times Review of Charm City'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/17/arts/17charmcity/17charmcity-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Horn from the Heart: The Paul Butterfield Story', 'mpaa_rating': '', 'critics_pick': 1, 'byline': 'GLENN KENNY', 'headline': 'Review: Paul Butterfield’s Story Is Told in ‘Horn From the Heart’', 'summary_short': 'A documentary explores the life of the blues musician who was prominent in the 1960s and ’70s.', 'publication_date': '2018-10-16', 'opening_date': '2018-10-19', 'date_updated': '2018-10-16 11:04:04', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/16/movies/horn-from-the-heart-review-paul-butterfield.html', 'suggested_link_text': 'Read the New York Times Review of Horn from the Heart: The Paul Butterfield Story'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/17/arts/17hornfromtheheart/17hornfromtheheart-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'The Price of Everything', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'A. O. SCOTT', 'headline': 'Review: ‘The Price of Everything’ Asks $56 Billion Questions About Art', 'summary_short': 'This documentary examines the global art market, and pauses to look at some pictures along the way.', 'publication_date': '2018-10-16', 'opening_date': '2018-10-19', 'date_updated': '2018-10-16 16:08:03', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/16/movies/the-price-of-everything-review-documentary.html', 'suggested_link_text': 'Read the New York Times Review of The Price of Everything'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/19/arts/19priceofeverything/19priceofeverything-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Impulso', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'BEN KENIGSBERG', 'headline': 'Review: ‘Impulso’ Goes Backstage With a Flamenco Innovator', 'summary_short': 'This documentary follows Rocío Molina, a cutting-edge dancer, as she prepares for a Paris show.', 'publication_date': '2018-10-16', 'opening_date': None, 'date_updated': '2018-10-16 11:04:03', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/16/movies/impulso-review-documentary.html', 'suggested_link_text': 'Read the New York Times Review of Impulso'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/17/arts/17impulso/17impulso-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Watergate', 'mpaa_rating': '', 'critics_pick': 1, 'byline': 'A.O. SCOTT', 'headline': 'Review: ‘Watergate’ Shocks Anew With Its True Tale of Political Scandal', 'summary_short': 'Charles Ferguson delivers a comprehensive documentary about the not-so-distant past, with its eye very much on the present.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:21', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/watergate-review-documentary.html', 'suggested_link_text': 'Read the New York Times Review of Watergate'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12watergate/12watergate-mediumThreeByTwo210-v3.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Barbara', 'mpaa_rating': '', 'critics_pick': 1, 'byline': 'GLENN KENNY', 'headline': 'Review: In ‘Barbara,’ a Fictional Biopic of a French Chanteuse', 'summary_short': 'It’s a film of scenes rather than of one unified narrative, but each scene is a showcase for the magnificent talents of its star.', 'publication_date': '2018-10-11', 'opening_date': None, 'date_updated': '2018-10-17 02:44:21', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/barbara-review.html', 'suggested_link_text': 'Read the New York Times Review of Barbara'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12barbara/merlin_144926925_2fb5b176-1b74-4549-9be7-251a1f04323d-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Over the Limit', 'mpaa_rating': '', 'critics_pick': 1, 'byline': 'JEANNETTE CATSOULIS', 'headline': 'Review: A Russian Gymnast Goes ‘Over the Limit’', 'summary_short': 'Margarita Mamun endures injury and abuse in Marta Prus’s brilliantly constructed documentary.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-05', 'date_updated': '2018-10-17 02:44:20', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/over-the-limit-review.html', 'suggested_link_text': 'Read the New York Times Review of Over the Limit'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12over1/12over1-mediumThreeByTwo210-v2.jpg', 'width': 210, 'height': 140}}, {'display_title': 'The Kindergarten Teacher', 'mpaa_rating': 'R', 'critics_pick': 1, 'byline': 'JEANNETTE CATSOULIS', 'headline': 'Review: The Disturbing Obsession of ‘The Kindergarten Teacher’', 'summary_short': 'Maggie Gyllenhaal is riveting as a dissatisfied teacher who’s obsessed with her 5-year-old pupil’s poetic talent.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:19', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/the-kindergarten-teacher-review.html', 'suggested_link_text': 'Read the New York Times Review of The Kindergarten Teacher'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12kindergarten1/kindergarten1-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Classical Period', 'mpaa_rating': '', 'critics_pick': 1, 'byline': 'BEN KENIGSBERG', 'headline': 'Review: In ‘Classical Period,’ a Deep Dive — Really Deep — Into Dante', 'summary_short': 'This highly original feature is technically in English, but it might as well be in liberal-arts-speak.', 'publication_date': '2018-10-11', 'opening_date': None, 'date_updated': '2018-10-17 02:44:18', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/classical-period-review.html', 'suggested_link_text': 'Read the New York Times Review of Classical Period'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/10/arts/classical1/classical1-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Bad Times at the El Royale', 'mpaa_rating': 'R', 'critics_pick': 0, 'byline': 'MANOHLA DARGIS', 'headline': 'Review: Hard-Boiled Play in ‘Bad Times at the El Royale’', 'summary_short': 'The writer-director Drew Goddard has fun with genre and a cast that includes Jeff Bridges, Dakota Johnson, Jon Hamm, Cynthia Erivo and Chris Hemsworth.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:22', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/bad-times-at-the-el-royale-review.html', 'suggested_link_text': 'Read the New York Times Review of Bad Times at the El Royale'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12badtimes-1/merlin_144926712_c4da8d26-b8af-4e7b-b65d-75e7ae46f296-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Beautiful Boy', 'mpaa_rating': 'R', 'critics_pick': 0, 'byline': 'A.O. SCOTT', 'headline': 'Review: In ‘Beautiful Boy,’ a Writer Confronts His Son’s Meth Addiction', 'summary_short': 'Two memoirs are brought to the screen in a father-son drama starring Steve Carell and Timothée Chalamet.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:21', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/beautiful-boy-review-steve-carell.html', 'suggested_link_text': 'Read the New York Times Review of Beautiful Boy'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12beautifulboy/merlin_144926952_7ed013e2-cd6b-44c0-9431-dc59fc305700-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'The Oath', 'mpaa_rating': 'R', 'critics_pick': 0, 'byline': 'GLENN KENNY', 'headline': 'Review: In ‘The Oath,’ a Pledge of Allegiance to a President Creates Chasms', 'summary_short': 'This satirical comedy, written, directed by and starring Ike Barinholtz, turns dark and ham-handed.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:21', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/the-oath-review-tiffany-haddish.html', 'suggested_link_text': 'Read the New York Times Review of The Oath'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12theoath/12theoath-mediumThreeByTwo210-v2.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Bikini Moon', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'KEN JAWOROWSKI', 'headline': 'Review: ‘Bikini Moon’ Finds a Documentary Crew Under Its Subject’s Spell', 'summary_short': 'Condola Rashad plays the title character, a homeless women who manipulates, and is manipulated by, filmmakers who soon have their own problems.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:20', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/bikini-moon-review.html', 'suggested_link_text': 'Read the New York Times Review of Bikini Moon'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12bikini1/12bikini1-mediumThreeByTwo210-v4.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Goosebumps 2: Haunted Halloween', 'mpaa_rating': 'PG', 'critics_pick': 0, 'byline': 'TEO BUGBEE', 'headline': 'Review: ‘Goosebumps 2: Haunted Halloween’ Is Toothless Terror', 'summary_short': 'This sequel to the movie adaptation of R.L. Stine’s horror series is more goofy than scary.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:20', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/goosebumps-2-haunted-halloween-review.html', 'suggested_link_text': 'Read the New York Times Review of Goosebumps 2: Haunted Halloween'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12goosebumps/merlin_144927237_ce38ea83-4672-4382-8c4d-e6c80325379c-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'The Sentence', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'KEN JAWOROWSKI', 'headline': 'Review: In ‘The Sentence,’ a Woman Gets Prison, Her Family Also Pays', 'summary_short': 'The documentary denounces minimum sentencing laws that put Cindy Shank behind bars.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:19', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/the-sentence-review.html', 'suggested_link_text': 'Read the New York Times Review of The Sentence'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/09/arts/thesentence1/thesentence1-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'All Square', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'GLENN KENNY', 'headline': 'Review: In ‘All Square,’ Taking Big Bets on Youth Baseball', 'summary_short': 'Michael Kelly, Pamela Adlon and Josh Lucas enhance the small-town bookmaking shenanigans of this comedy-drama.', 'publication_date': '2018-10-11', 'opening_date': None, 'date_updated': '2018-10-11 11:04:11', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/all-square-review.html', 'suggested_link_text': 'Read the New York Times Review of All Square'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12allsquare/12allsquare-mediumThreeByTwo210-v2.jpg', 'width': 210, 'height': 140}}, {'display_title': 'Sadie', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'KEN JAWOROWSKI', 'headline': 'Review: The Drama ‘Sadie’ Finds a Teenager in a Tough Situation', 'summary_short': 'The film stars Sophia Mitri Schloss as the title character, a 13-year-old girl who grows angry at the men who are courting her mother.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-11 11:04:07', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/sadie-review.html', 'suggested_link_text': 'Read the New York Times Review of Sadie'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12sadie1/sadie1-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'After Everything', 'mpaa_rating': '', 'critics_pick': 0, 'byline': 'TEO BUGBEE', 'headline': 'Review: In ‘After Everything,’ a Young Love Blooms in Crisis', 'summary_short': 'This cancer drama focuses less on the high stakes of illness than on how two young people talk to each other in sickness and in health.', 'publication_date': '2018-10-11', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:18', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/11/movies/after-everything-review.html', 'suggested_link_text': 'Read the New York Times Review of After Everything'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12aftereverything/12aftereverything-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}, {'display_title': 'First Man', 'mpaa_rating': 'PG-13', 'critics_pick': 0, 'byline': 'A.O. SCOTT', 'headline': 'Review: ‘First Man’ Takes a Giant Leap for Man, a Smaller Step for Movies', 'summary_short': 'Damien Chazelle’s sweeping and intimate yet underwhelming film revisits the first lunar landing, with Ryan Gosling as Neil Armstrong.', 'publication_date': '2018-10-10', 'opening_date': '2018-10-12', 'date_updated': '2018-10-17 02:44:18', 'link': {'type': 'article', 'url': 'http://www.nytimes.com/2018/10/10/movies/first-man-review-ryan-gosling-damien-chazelle.html', 'suggested_link_text': 'Read the New York Times Review of First Man'}, 'multimedia': {'type': 'mediumThreeByTwo210', 'src': 'https://static01.nyt.com/images/2018/10/12/arts/12FIRSTMAN-1/merlin_144926997_3122f50f-2561-4ea3-918c-f6911d00c31f-mediumThreeByTwo210.jpg', 'width': 210, 'height': 140}}]
    
    
    
    



```python
movies_data["results"][0]['link']['url']
```




    'http://www.nytimes.com/2018/10/16/movies/can-you-ever-forgive-me-review-melissa-mccarthy.html'



## How many unique critics are there?


```python
#Your code here
critics = []
for x in movies_data['results']:
    critics.append(x['byline'])
print(critics)
len(critics)
```

    ['A.O. SCOTT', 'BEN KENIGSBERG', 'GLENN KENNY', 'A. O. SCOTT', 'BEN KENIGSBERG', 'A.O. SCOTT', 'GLENN KENNY', 'JEANNETTE CATSOULIS', 'JEANNETTE CATSOULIS', 'BEN KENIGSBERG', 'MANOHLA DARGIS', 'A.O. SCOTT', 'GLENN KENNY', 'KEN JAWOROWSKI', 'TEO BUGBEE', 'KEN JAWOROWSKI', 'GLENN KENNY', 'KEN JAWOROWSKI', 'TEO BUGBEE', 'A.O. SCOTT']





    20




```python
# get uniqueness using a list and an if statement
critics = []
for result in movies_data['results']:
    author = result['byline']
    if author not in critics:
        critics.append(author)
print(critics)
len(critics)
```

    ['A.O. SCOTT', 'BEN KENIGSBERG', 'GLENN KENNY', 'A. O. SCOTT', 'JEANNETTE CATSOULIS', 'MANOHLA DARGIS', 'KEN JAWOROWSKI', 'TEO BUGBEE']





    8




```python
# use a set!
critics = set()
for result in movies_data['results']:
    author = result['byline'].replace(" ", "")
    critics.add(author)
print(critics)
len(critics)
```

    {'BENKENIGSBERG', 'GLENNKENNY', 'TEOBUGBEE', 'A.O.SCOTT', 'KENJAWOROWSKI', 'JEANNETTECATSOULIS', 'MANOHLADARGIS'}





    7




```python
critics_srs = pd.Series(critics)
critics_srs.value_counts().shape[0]
```




    8



## Create a new column for the review's url. Title the column 'review_url'


```python
#Your code here
for result in movies_data['results']:
    result['review_url'] = result['link']['url']
```


```python
movies_data['results'][0]['review_url']
```




    'http://www.nytimes.com/2018/10/16/movies/can-you-ever-forgive-me-review-melissa-mccarthy.html'



## How many results are in the file? 


```python
#Your code here
len(movies_data['results'])
```




    20




```python
f = open("new_ny_data_movies.json", 'w')
```


```python
json.dump(movies_data, f)
```


```python
f.close()
```

## Summary
Well done! Here you continued to gather practice extracting data from JSON files and transforming them into our standard tool of Pandas DataFrames.
