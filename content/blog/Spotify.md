+++
categories = ["tutorial"]
date = "2020-01-30"
description = "Tutorial on how to analyze your Spotify data."
title = "Spotify Data Analysis"
type = "post"
draft = false

+++

After Spotify did their end-of-the-year summary of my listening history, I was inspired to do more analysis on my listening data. Instead of just including the output of my work, I am going to go through my code to provide an easy-to-follow resource if you're a programmer who is new to Python.

If you request it, Spotify will let you download a year's worth of listening history. I was so excited by all this data that I told my coworker Victor about it, and got him just as interested in doing this data analysis! I want to give him credit for helping me clean up a couple of my functions, and for giving me the idea to look for skipped and most-skipped songs. 

I'm using Jupyter Notebook for this data analysis. Once you download your data, save it into a file named 'data'.

```
import pathlib

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

root = pathlib.Path('./data')
```

First, let's create a function that will convert all of your streaming history from .json objects into cool pandas data frames!

```
def load_streaming_data(root):
    dfs = [pd.read_json(p, encoding='utf-8') for p in root.glob('StreamingHistory*.json')]
    return pd.concat(dfs).reset_index(drop=True)
```

Now, let's select our 'endTime' column in our data frame and account for your timezone.

```
df = load_streaming_data(root)
df['endTime'] = pd.to_datetime(df['endTime'])

df['endTime'].dt.tz_localize('UTC', ambiguous='infer').dt.tz_convert('US/Pacific')
```

## Skipped Songs

So our data frame right now has four columns: endTime, artistName, trackName, and msPlayed. Let's add one more column -- skipped songs. Let's say the criteria for a song to be skipped is if you have listened to less than 30 seconds of it.

```
df['Skipped'] = df['msPlayed'] < 1000 * 30 #remember that we are given milliseconds
```

Okay, so now we have a column that tells us whether or not a song is skipped. Let's take this information and find out the percentage that each song in our listening history has been skipped.

```
grp = df.groupby(['artistName', 'trackName'])

# only include songs that have at least 15 plays
df_agg = (grp['Skipped'].sum() / grp.size()) [grp.size() > 15]

df_agg.sort_values(ascending=False).head(10)
```

![Example image](/most_skipped.png)

This is the top ten most-skipped songs that I actually listen to (which is why I only included songs that I have played at least 15 times).

## Top Songs

Spotify gives your top five songs in their wrap-up. I was curious about my top ten songs, and wanted to see if my top-five ranking would match up with Spotify's.

```
df_played = df[df['Skipped'] == False] 
df_played.groupby(['artistName', 'trackName']).size().sort_values(ascending=False).head(10)
```

![top songs](/top_songs.png)

The first five on this list are the same as the top five songs that Spotify told me! 

## Most Skipped-To Songs
Now that we know which songs are the most skipped, it begs the question..are there certain songs that you'll often skip to? Let's find out!

The logic behind finding these songs is that if the previous song was skipped, the current song wasn't skipped.

```
m = df['Skipped'].shift(1) & ~df['Skipped']
df_skipped_to = df[m]

grp = df_skipped_to.groupby(['artistName', 'trackName'])

agg = grp.size()
agg.sort_values(ascending=False).head(10)
```

![most skipped-to songs](/skipped_to_songs.png)

Interesting! There is some overlap between my most skipped-to songs and my top songs of the year.

## Map time-of-day to most-listened-to songs
I came up with categories for time of day and included only non-skipped songs. In my original calculations, I had included all songs, and it wasn't until my coworker(/collaborator) Victor pointed it out that I realized it makes more sense for my analysis to only look for non-skipped songs. Since I am aiming to find out which songs I'm listening to at a given time of day, I probably want to look at the results of songs I was _actually_ listening to. This is a good example of how data analysis isn't straightforward; changing the parameters of what data you're analyzing can shape your results in ways you don't realize. 


**morning:** 6:00AM-11:59AM  
**afternoon:** 12:00PM-5:59PM  
**evening:** 6:00PM-11:59PM  
**late-night:** 12AM-5:59AM  

```
df_played = df[df['Skipped'] == False]
times = df_played['endTime'].dt.time
```

```
def time_analysis(df, time_of_day):    
    df_played = df[df['Skipped'] == False] 
    times = df_played['endTime'].dt.time
    
    # could turn into a switch statement to make it faster
    if time_of_day.lower() == 'morning':
        start = "06:00:00"
        end = "11:59:59"
    elif time_of_day.lower() == 'afternoon':
        start = "11:59:59"
        end = "17:59:59"        
    elif time_of_day.lower() == 'evening':
        start = "17:59:59"
        end = "23:59:59"
    elif time_of_day.lower() == 'night':
        start = "00:00:00"
        end = "05:59:59"
    else:
        return "error!!! options are 'morning', 'afternoon', 'evening', 'night'"
        
    mask = (times > pd.to_datetime(start).time()) & (times <= pd.to_datetime(end).time())
    df_calc = df_played[mask]

    grouped = df_calc.groupby(['artistName', 'trackName'])
    aggr = grouped.size()
    return aggr.sort_values(ascending=False).head(10)
```

So, for our songs listened to in the morning:
```
time_analysis(df, 'morning')
```

![morning result](/morning.png)

versus the songs I listened to in the evening:
```
time_analysis(df, 'evening')
```

![evening result](/evening.png)

The natural next step was to write a function that does this calculation for the time of day and day of the week. Here is my version below:

```
def time_and_day(df, time, day):    
    df_played = df[df['Skipped'] == False] 
    times = df_played['endTime'].dt.time
    
    if time.lower() == 'morning':
        start = "06:00:00"
        end = "11:59:59"
    elif time.lower() == 'afternoon':
        start = "11:59:59"
        end = "17:59:59"        
    elif time.lower() == 'evening':
        start = "17:59:59"
        end = "23:59:59"
    elif time.lower() == 'night':
        start = "00:00:00"
        end = "05:59:59"
    else:
        return "error!!! options are 'morning', 'afternoon', 'evening', 'night'"
        
    mask = (df_played['endTime'].dt.day_name() == day) & (times > pd.to_datetime(start).time()) & (times <= pd.to_datetime(end).time())
    df_calc = df_played[mask]

    grouped = df_calc.groupby(['artistName', 'trackName'])
    aggr = grouped.size()
    return aggr.sort_values(ascending=False).head(10)
```

Here is what I listen to on a Monday morning:

```
time_and_day(df, 'morning', 'Monday')
```
![Monday morning result](/monday_morning.png)

versus what songs I was most listening to on a Thursday afternoon:

```
time_and_day(df, 'afternoon', 'Thursday')
```
![Thursday afternoon result](/thurs_afternoon.png)


And now you've done some basic data analysis on your listening history using Python! There's more that could be done (heatmaps of artists, visualizing time-of-day, flipping the skipped-song parameter to analyze which songs you're likely to skip, etc.), but I'll end this here for now, and maybe do a part 2 with more complex examples.