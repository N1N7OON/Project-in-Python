![Movie popcorn on red background](Dataset/redpopcorn.jpg)

**Netflix**! What started in 1997 as a DVD rental service has since exploded into one of the largest entertainment and media companies.

Given the large number of movies and series available on the platform, it is a perfect opportunity to flex your exploratory data analysis skills and dive into the entertainment industry. Our friend has also been brushing up on their Python skills and has taken a first crack at a CSV file containing Netflix data. They believe that the average duration of movies has been declining. Using your friends initial research, you'll delve into the Netflix data to see if you can determine whether movie lengths are actually getting shorter and explain some of the contributing factors, if any.

You have been supplied with the dataset `netflix_data.csv` , along with the following table detailing the column names and descriptions:

## The data
### **netflix_data.csv**
| Column | Description |
|--------|-------------|
| `show_id` | The ID of the show |
| `type` | Type of show |
| `title` | Title of the show |
| `director` | Director of the show |
| `cast` | Cast of the show |
| `country` | Country of origin |
| `date_added` | Date added to Netflix |
| `release_year` | Year of Netflix release |
| `duration` | Duration of the show in minutes |
| `description` | Description of the show |
| `genre` | Show genre |


```python
# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

# Start coding!
```


```python
netflix_df = pd.read_csv("netflix_data.csv")
netflix_df[0:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>duration</th>
      <th>description</th>
      <th>genre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>s1</td>
      <td>TV Show</td>
      <td>3%</td>
      <td>NaN</td>
      <td>João Miguel, Bianca Comparato, Michel Gomes, R...</td>
      <td>Brazil</td>
      <td>August 14, 2020</td>
      <td>2020</td>
      <td>4</td>
      <td>In a future where the elite inhabit an island ...</td>
      <td>International TV</td>
    </tr>
    <tr>
      <th>1</th>
      <td>s2</td>
      <td>Movie</td>
      <td>7:19</td>
      <td>Jorge Michel Grau</td>
      <td>Demián Bichir, Héctor Bonilla, Oscar Serrano, ...</td>
      <td>Mexico</td>
      <td>December 23, 2016</td>
      <td>2016</td>
      <td>93</td>
      <td>After a devastating earthquake hits Mexico Cit...</td>
      <td>Dramas</td>
    </tr>
    <tr>
      <th>2</th>
      <td>s3</td>
      <td>Movie</td>
      <td>23:59</td>
      <td>Gilbert Chan</td>
      <td>Tedd Chan, Stella Chung, Henley Hii, Lawrence ...</td>
      <td>Singapore</td>
      <td>December 20, 2018</td>
      <td>2011</td>
      <td>78</td>
      <td>When an army recruit is found dead, his fellow...</td>
      <td>Horror Movies</td>
    </tr>
    <tr>
      <th>3</th>
      <td>s4</td>
      <td>Movie</td>
      <td>9</td>
      <td>Shane Acker</td>
      <td>Elijah Wood, John C. Reilly, Jennifer Connelly...</td>
      <td>United States</td>
      <td>November 16, 2017</td>
      <td>2009</td>
      <td>80</td>
      <td>In a postapocalyptic world, rag-doll robots hi...</td>
      <td>Action</td>
    </tr>
    <tr>
      <th>4</th>
      <td>s5</td>
      <td>Movie</td>
      <td>21</td>
      <td>Robert Luketic</td>
      <td>Jim Sturgess, Kevin Spacey, Kate Bosworth, Aar...</td>
      <td>United States</td>
      <td>January 1, 2020</td>
      <td>2008</td>
      <td>123</td>
      <td>A brilliant group of students become card-coun...</td>
      <td>Dramas</td>
    </tr>
    <tr>
      <th>5</th>
      <td>s6</td>
      <td>TV Show</td>
      <td>46</td>
      <td>Serdar Akar</td>
      <td>Erdal Beşikçioğlu, Yasemin Allen, Melis Birkan...</td>
      <td>Turkey</td>
      <td>July 1, 2017</td>
      <td>2016</td>
      <td>1</td>
      <td>A genetics professor experiments with a treatm...</td>
      <td>International TV</td>
    </tr>
    <tr>
      <th>6</th>
      <td>s7</td>
      <td>Movie</td>
      <td>122</td>
      <td>Yasir Al Yasiri</td>
      <td>Amina Khalil, Ahmed Dawood, Tarek Lotfy, Ahmed...</td>
      <td>Egypt</td>
      <td>June 1, 2020</td>
      <td>2019</td>
      <td>95</td>
      <td>After an awful accident, a couple admitted to ...</td>
      <td>Horror Movies</td>
    </tr>
    <tr>
      <th>7</th>
      <td>s8</td>
      <td>Movie</td>
      <td>187</td>
      <td>Kevin Reynolds</td>
      <td>Samuel L. Jackson, John Heard, Kelly Rowan, Cl...</td>
      <td>United States</td>
      <td>November 1, 2019</td>
      <td>1997</td>
      <td>119</td>
      <td>After one of his high school students attacks ...</td>
      <td>Dramas</td>
    </tr>
    <tr>
      <th>8</th>
      <td>s9</td>
      <td>Movie</td>
      <td>706</td>
      <td>Shravan Kumar</td>
      <td>Divya Dutta, Atul Kulkarni, Mohan Agashe, Anup...</td>
      <td>India</td>
      <td>April 1, 2019</td>
      <td>2019</td>
      <td>118</td>
      <td>When a doctor goes missing, his psychiatrist w...</td>
      <td>Horror Movies</td>
    </tr>
    <tr>
      <th>9</th>
      <td>s10</td>
      <td>Movie</td>
      <td>1920</td>
      <td>Vikram Bhatt</td>
      <td>Rajneesh Duggal, Adah Sharma, Indraneil Sengup...</td>
      <td>India</td>
      <td>December 15, 2017</td>
      <td>2008</td>
      <td>143</td>
      <td>An architect and his wife move into a castle t...</td>
      <td>Horror Movies</td>
    </tr>
  </tbody>
</table>
</div>




```python
netflix_subset = netflix_df[netflix_df["type"] == "Movie"]
print(netflix_subset.head(5))
```

      show_id  ...          genre
    1      s2  ...         Dramas
    2      s3  ...  Horror Movies
    3      s4  ...         Action
    4      s5  ...         Dramas
    6      s7  ...  Horror Movies
    
    [5 rows x 11 columns]
    


```python
netflix_movies = netflix_subset[["title","country", "genre", "release_year","duration"]]
print(netflix_movies.head(5))
```

       title        country          genre  release_year  duration
    1   7:19         Mexico         Dramas          2016        93
    2  23:59      Singapore  Horror Movies          2011        78
    3      9  United States         Action          2009        80
    4     21  United States         Dramas          2008       123
    6    122          Egypt  Horror Movies          2019        95
    


```python
short_movies = netflix_movies[netflix_movies["duration"] < 60]
print(short_movies.head(20))
```

                                                     title  ... duration
    35                                           #Rucker50  ...       56
    55                 100 Things to do Before High School  ...       44
    67   13TH: A Conversation with Oprah Winfrey & Ava ...  ...       37
    101                                  3 Seconds Divorce  ...       53
    146                                     A 3 Minute Hug  ...       28
    162  A Christmas Special: Miraculous: Tales of Lady...  ...       22
    171                         A Family Reunion Christmas  ...       29
    177                    A Go! Go! Cory Carson Christmas  ...       22
    178                    A Go! Go! Cory Carson Halloween  ...       22
    179                  A Go! Go! Cory Carson Summer Camp  ...       21
    181             A Grand Night In: The Story of Aardman  ...       59
    200                            A Love Song for Latasha  ...       20
    220                         A Russell Peters Christmas  ...       44
    233                              A StoryBots Christmas  ...       26
    237                             A Tale of Two Kitchens  ...       30
    242                            A Trash Truck Christmas  ...       28
    247                            A Very Murray Christmas  ...       57
    285                               Abominable Christmas  ...       44
    295                                 Across Grace Alley  ...       24
    305                Adam Devine: Best Time of Our Lives  ...       59
    
    [20 rows x 5 columns]
    


```python
colors = []
for lab, row in netflix_movies.iterrows():
    if row["genre"] == "Children":
         colors.append("Blue")
    elif row["genre"] == "Documentaries":
         colors.append("Orange")
    elif row["genre"] == "Stand-Up":
        colors.append("Green")
    else :
        colors.append("Pink")
    
print(colors)
```

    ['Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Blue', 'Green', 'Orange', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Orange', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Green', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Blue', 'Pink', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Green', 'Orange', 'Orange', 'Blue', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Orange', 'Blue', 'Orange', 'Blue', 'Orange', 'Orange', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Orange', 'Green', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Green', 'Orange', 'Blue', 'Orange', 'Blue', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Green', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Orange', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Orange', 'Pink', 'Green', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Green', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Green', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Orange', 'Green', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Orange', 'Orange', 'Orange', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Green', 'Green', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Orange', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Orange', 'Blue', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Green', 'Pink', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Orange', 'Blue', 'Green', 'Green', 'Green', 'Orange', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Blue', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Green', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Green', 'Orange', 'Pink', 'Orange', 'Blue', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Orange', 'Blue', 'Orange', 'Orange', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Orange', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Green', 'Green', 'Green', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Green', 'Green', 'Orange', 'Orange', 'Orange', 'Green', 'Green', 'Orange', 'Green', 'Pink', 'Blue', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Orange', 'Green', 'Green', 'Blue', 'Pink', 'Blue', 'Blue', 'Orange', 'Pink', 'Green', 'Green', 'Green', 'Pink', 'Orange', 'Green', 'Green', 'Pink', 'Orange', 'Green', 'Green', 'Green', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Blue', 'Green', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Blue', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Green', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Orange', 'Blue', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Blue', 'Blue', 'Blue', 'Blue', 'Orange', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Green', 'Green', 'Blue', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Green', 'Orange', 'Orange', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Green', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Green', 'Green', 'Green', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Blue', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Blue', 'Pink', 'Pink', 'Blue', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Pink', 'Pink', 'Green', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Green', 'Blue', 'Blue', 'Blue', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Green', 'Orange', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Green', 'Green', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Pink', 'Orange', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Orange', 'Green', 'Pink', 'Pink', 'Blue', 'Orange', 'Orange', 'Blue', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Green', 'Blue', 'Green', 'Green', 'Pink', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Green', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Orange', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Blue', 'Blue', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Blue', 'Pink', 'Orange', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Green', 'Orange', 'Pink', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Blue', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Blue', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Blue', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Green', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Orange', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Blue', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Green', 'Green', 'Green', 'Pink', 'Orange', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Blue', 'Green', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Orange', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Green', 'Green', 'Orange', 'Pink', 'Pink', 'Orange', 'Orange', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Blue', 'Blue', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Orange', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Green', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Blue', 'Green', 'Green', 'Blue', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Green', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Pink', 'Orange', 'Blue', 'Orange', 'Pink', 'Blue', 'Pink', 'Pink', 'Blue', 'Pink', 'Pink', 'Orange', 'Orange']
    


```python
fig = plt.figure(figsize=(12,8))
plt.scatter(netflix_movies.release_year, netflix_movies.duration, c=colors)
plt.title("Movie Duration by Year of Release")
plt.xlabel("Release year")
plt.ylabel("Duration (min)")
plt.show()

```


    
![png](Dataset/output_8_0.png)
    



```python
answer = "no"
```

