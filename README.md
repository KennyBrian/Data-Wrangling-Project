# Data-Wrangling-Project

## Gathering Datasets
Three datasets were Gathered for analysis, namely:
- Twitter-Archive-Enhanced
- Image-Predictions
- Tweet-Json

## Assesing
The datasets were assessed visually and programmatically, and following issues were identified for cleaning:

**Quality issues**

- twitter_archive- source column has html tags
- twitter_archive- includes retweets and replies to tweets
- twitter_archive- wrong data source in the source column.
- twitter_archive - wrong data type for tweet_id, in_reply_to_status_id, in_reply_to_user_id, timestamp, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp
- twitter_archive - name has repeated name 'a'
- twitter_archive - extract these ratings by taking the ratio of numerator and denominator
- twitter_archive - for the expanded_urls column, some of the urls have been entered more than once
- DECIMAL DOG RATINGS wrong entries where there are decimals in the rating

**Tidiness issues**

- twitter_archive - dog stages are in differents columns. we have dogs in multiple stages
- merging the three data sets into one

## Cleaning
First, I made the copies of the data using .copy(). Then I removed the retweets and replies to tweets by selecting the row that were null for retweeted_status_id & 
in_reply_to_status_id. I followed this up by removing all the columns related to retweets and replies to tweets. Secondly, I changed a few columns to correct 
datatype. First, the tweet_id column datatype to string for the three datasets using astype(str) functionality then the timestamp column to datatype using 
pd.to_datetime(). The source column had html tags in the texts. To remove these,I first split the strings using the series split method str.split() with " as the 
seperator and then selected the first entry in the resulting list using [1]. From this column, i dropped the rows whose url was 'http://vine.co' using regex 
function, str.match('http://vine.co') ==False. the rationale for this was that we need the tweets from weratedog handle in twitter.For the tweete whose rating had a 
decimal, the numerator was entered wrongly by taking the value after the decimal. I filtered these using the regex function (\d+.\d/\d+), extracted the correct 
rating from the text amended the rating numerator using using *.loc. Since the rating denominator is not equal for all rows, I calculated the rating by geting the
ratio of the rating numerator and denominator.
I also converted the duplicated name a in the name column to NaN using the replace method. Some entries in the expanded_urls had urle entered more that once in a 
single row. to clean these, I first split these entries using the series split method str.split(',', expand=True) using ',' as the seperator and then selected the 
first column using [0]. the dogs stages need to merged to one list. I first converted the None entries into empty strings using the replace method replace('None', 
'', inplace=True) for the four columns with dog stages then merged the columns with the different dog stages using string concatenation. since some rows had multiple
stages and concating would distort these stages, i corrected the dog stages using by locating and amending the the naming. Finally, I dropped the doggo, floofer, 
pupper, puppo columns using the .drop() method.
All the datasets need to be in one dataset so i merged the 3 datasets using on the tweet_id column.
