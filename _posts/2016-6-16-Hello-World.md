---
layout: post
title: DSI-HK-1
---

This is the second project.

## Step 1: Exploring your data.
- The data is about the Year 2000 billboard (top 100 tracks).
- There are 316 tracks, with year, artist, track name, time, genre, date entered, date peaked, and rank from 1st to 76th week.
- It has when the track was entered and when it exited the billboard. Jay\_z has the most tracks (5 tracks) which entered the billboard. There are 228 artists which has entered the billboard. There are 10 types of genre of music with Rock being most popular. There are songs which entered the billboard in 1999 and exited 2000 and also entered in 2000 and exited in 2001.
- I found that all dates are Saturdays.

## Step 2: Clean your data.
- I found that for the year column it is all 2000, so we can drop this column.
- I cleaned the titles such as 'date.entered' becomes 'date\_entered', 'x1st.week' becomes 'week\_1'.
- There is a track which has identical name by two different artists. So, I append the artist name after the track name.
- When I melted the table into three columns 'track', 'week', and 'rank', I change the 'week' into integer. 
- I also added the 'date' column, so week 1 will be the date entered and week 2 will be the date entered plus 7 days.

```python
track_rank_table['date'] = np.array([None]*len(track_rank_table))
for i in range(0,76):
    k = 0
    for j in range(len(df_clean)*i, len(df_clean)*(i+1)):       
        track_rank_table.ix[j,'date'] = df_clean.ix[k, 'date_entered'] + datetime.timedelta(days = (7*(i)))
        k = k + 1
```

![](https://raw.githubusercontent.com/tkjyeung/tkjyeung.github.io/e8b87b6b126bd1736c4550fdf7c87cd5d42cea94/images/track_rank_table.PNG)

- We are only interested in year 2000 billboard and also need to clean nan rank track rows.
- track\_rank\_table\_info\_clean only has the track info which is within year 2000 and zero nan rank track.

## Step 3: Visualize your data.

- Since there are way too many tracks. I just plotted the tracks which has reached top 1 and their trend developments.

![]({{ site.baseurl }}/images/track-rank-by-week.JPG)

- Let's explore audience taste trend over the year 2000.

![]({{ site.baseurl }}/images/time.JPG)

- This shows that people favour shorter and shorter time tracks towards year end.

![]({{ site.baseurl }}/images/track_word_len.JPG)

- Shorter track name works better towards year end.

![]({{ site.baseurl }}/images/artist_word_len.JPG)

- Artist name length does not matter.

![]({{ site.baseurl }}/images/artist_on_billboard.JPG)

- Due to too many tracks cluttering the bar graph, I decided to set minimum to be at least 50 occurances.
Destiny's Child appears most the billboard in 2000. Creed is 2nd place.

## Step 4: Create a Problem Statement.

##### Having explored the data, come up with a problem statement for this data set. You can feel free to introduce data from any other source to support your problem statement, just be sure to provide a link to the origin of the data. Once again- be creative!


## Step 5: Brainstorm your Approach.
##### In bullet-list form, provide a proposed approach for evaluating your problem statement. This can be somewhat high-level, but start to think about ways you can massage the data for maximum efficacy. 