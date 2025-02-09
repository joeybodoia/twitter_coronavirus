# Coronavirus twitter analysis

## Data/Background
Approximately 500 million tweets are sent everyday. Of those tweets, about 1% are *geotagged*. The data used for this project was all of the *geotagged* tweets sent in 2020, which was on the order of 1.1 billion tweets.

## Project Overview
For this project, I followed the *MapReduce* procedure to analyze the dataset of tweets in order to compare, by language and country, the number of tweets that included corona virus related hashtags.
Here are the hashtags that were considered:
```
hashtags = [
    '#코로나바이러스',  # korean
    '#コロナウイルス',  # japanese
    '#冠状病毒',        # chinese
    '#covid2019',
    '#covid-2019',
    '#covid19',
    '#covid-19',
    '#coronavirus',
    '#corona',
    '#virus',
    '#flu',
    '#sick',
    '#cough',
    '#sneeze',
    '#hospital',
    '#nurse',
    '#doctor',
    ]
```
 The *MapReduce* procedure consisted of three main steps. First, the tweets were partitioned into 366 zip files, each containing the tweets for that day of the 2020 leap year. Next, a mapping file, `map.py`, was created that parsed over all of the tweets in a zip file, counting the number of languages and countries that had tweets involving the corona virus hashtags, writing the results to an outputs file. The last step was to reduce, or merge, all of the outputs generated by running the `map.py` file on all of the 366 zip files, into one combined output, which was done using the `reduce.py` file.
 
<img src=mapreduce.png width=100% />



## Design decisions
In order run my `map.py` function over all of the 366 zip files in parallel, I created a bash script, `run_maps.sh` that iterated over all of the zip files, instructing each iteration to run the `map.py` on that file in the background, using the `&` bash command. 

## Results
The results can be found in the `viz` folder. Inside, there is a `country` folder, and a `lang` folder. The `country` folder has a file for each hashtag, which maps country abbreviations to the number of tweets that included that hashtag. The `lang` folder also has a file for each hashtag, which, similarly, maps language abbreviations to the number of tweets that incuded that hashtag.

