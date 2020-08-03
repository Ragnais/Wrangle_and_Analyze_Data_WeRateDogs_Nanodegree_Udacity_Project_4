# Wrangle_and_Analyze_Data_WeRateDogs_Nanodegree_Udacity_Project_4
Introduction

The tasks in this project are as follows:

I. Data wrangling, which consists of:

  1.Gathering data;
  
  2.Assessing data;
  
  3.Cleaning data.

II. Storing, analyzing, and visualizing the wrangled data;


III. Reporting on:

    1.The data wrangle_report.pdf;
    
    2.The data analyses and visualizations act_report.pdf.

Part I. Data wrangling

1.Gathering data
Gather each of the three pieces of data:

twitter_archive_enhanced.csv - the WeRateDogs Twitter archive;

image_predictions.tsv - the tweet image predictions. The file can be downloaded programmatically using the Requests library and the following URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv

Each tweet's retweet count and favorite ("like") count at minimum, and any additional data we find interesting. Using the tweet IDs in the WeRateDogs Twitter archive, we query the Twitter API for each tweet's JSON data using Python's Tweepy library and store each tweet's entire set of JSON data in a file called tweet_json.txt file. Each tweet's JSON data should be written to its own line. 
Then we read this .txt file line by line into a pandas DataFrame with (at minimum) tweet ID, retweet count, and favorite count.

The below  Quality and Tidiness Issues were identified for further cleaning:

Quality Issues

DF: df_tw_archive

1.Incorrect data type for timestamp and retweeted_status_timestamp => Change to datetime

2.Replace: 'O' to 'O'Malley'; 'Al' to 'Al Cabone'; 'my' to 'Zoey'

3.We want to have only original ratings (no retweets) that have images => Remove 'retweeted_status_id' is not null and Remove columns 'retweeted_status_id', 'retweeted_status_user_id', 'retweeted_status_timestamp'

4.Column Name include invalid names "a", "an", "None", "the" etc. => Retrieve and Replace with the 'named' and 'name is' from 'text' col.

5.If there are still 'None' missing values in 'name' => Change from 'None' to NaN.

6.The columns rating_denominator and rating_numerator have invalid values:
#313 13/10 second pos; #1068 14/10 second pos; #1165 13/10 second pos; #1202 11/10 second pos; #1662 10/10 second pos; #2335 9/10 second pos
=> Correct positions where denominator is not 10 and where the text gives the correct rating by retrieving the second pos as a rating and change denominator and numerator correspondingly

DF: image_predictions

1.According to the p1-dog, p2-dog and p3-dog together, there are 324 rows with no dog on the picture => Delete 324 rows

2.The p1,p2 and p3 include Uppercase and Lowercase for the first letter => Replace first letter with Uppercase


DF: tweet_info

1.Rename id to tweet_id

2.Drop duplicates - 5631

Tidiness Issues
DF: df_tw_archive

1.One column 'Stage' : doggo, floofer, pupper, puppo => Create a new variable – 'Stage' to show the four dog stages, drop the four columns, and fill the empty with NaN.
tweet_info:

2.Join tweet_info with df_tw_archive and image_predictions


II. Storing, analyzing, and visualizing the wrangled data;

For the Analyze and Visualize, the next questions were targeted:

1.The most popular dog stage

2.The most populat breed of a dog

3.The most favourited/retweeted tweet

4.The correlation between ‘retweet_count’ and ‘favorite_count’.

Conclusion

Based on the data, the Retrievers at the pupper and doggo stages are likely to get the better ratings.

References:

https://kanoki.org/2019/11/12/how-to-use-regex-in-pandas/ -How to use Regex in Pandas
https://stackoverflow.com/questions/13851535/delete-rows-from-a-pandas-dataframe-based-on-a-conditional-expression-involving - How to delete rows from a pandas DataFrame based on a conditional expression
https://www.geeksforgeeks.org/split-a-string-into-columns-using-regex-in-pandas-dataframe/ - Split a String into columns using regex in pandas DataFrame
https://stackoverflow.com/questions/21943688/replace-nans-in-one-column-with-string-based-on-value-in-another-column - Replace NaN's in one column with string, based on value in another column
