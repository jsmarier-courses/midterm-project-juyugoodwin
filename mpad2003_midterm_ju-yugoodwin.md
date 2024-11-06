**November 5th 2024**<br>
**MPAD2003: Introductory Data Storytelling**<br>
**Ju-Yu Goodwin**<br>
**Presented to Jean-Sébastien Marier**<br>

# Midterm Project: Exploratory Data Analysis (EDA)

## 1. Introduction

In this assignment, I will be analyzing the dataset of [ 2024 service requests filed to The City of Ottawa](https://open.ottawa.ca/documents/65fe42e2502d442b8a774fd3d954cac5/about). Since this dataset is too big to work within Google Sheets, I will be using a modified version which you can see [here](https://raw.githubusercontent.com/jsmarier/course-datasets/refs/heads/main/ottawa-311-service-requests-august-2024.csv). I will be analyzing this dataset in four sections. Firstly getting data, understanding data, potential story and finally a conclusion.  

The service requests were taken and counted by four different places either residents could go to the 311 Contact Centre or Client Service Centre, or online with the 311 Email or Web-based Self-service portal. The dataset includes additional information about the service requests like the date that it was filed. Also, the status, if it was resolved or active. The type of service that has been requested is listed alongside a short description. And finally, it says how the service was called in.

## 2. Getting Data

First, I had to get the data. So I downloaded the CSV file and created a [new Google Sheets document](https://docs.google.com/spreadsheets/d/16TlAe4n38UvMbDcZgShybguWw8TvqVGhljz7YhPRdwQ/edit?usp=sharingto) put it in. Then in the new document, I imported the dataset by clicking on "File", found in the top right corner. Then I hit import. After clicking on import, the following page will pop up. Then you hit on upload.

![alt text](<Screenshot 2024-11-04 194910.png>)<br>
*Figure 1: The "Upload" button on Google Sheets to import a file.*

Once you hit upload, all your files will pop up. That's when you click on the CSV file. It should then automatically import it.

![alt text](<Screenshot 2024-11-04 194942.png>)<br>
*Figure 2: The downloads in your file explorer.*

After uploading it, the document should look like this:

![alt text](<Screenshot 2024-11-04 191726.png>)<br>
*Figure 3: The 2024 Service Requests dataset after you import it*

In this dataset, there are 274310 rows and 11 columns. At first glance, the data looks clean. The elements in each section seem to keep the same template and form of organization.

I am referencing the Government of Canada's Statistics: Power from Data! (2011) to explain each type of variable in this dataset. 

Columns B, C, D, G and K are all nominal variables. They each represent a category, name or label with no specific ordering. Column G contains addresses and can be considered an ordinal variable but since it is hard to notice any kind of order. I do not consider it to be in this case. It would be different if they all had the same street names.

Columns A, E and F are ordinal variables. Since columns E and F are dates and show a chronological order. And column A, shows the ID number of each service request which also follows a chronological order.

In columns I and H, we're dealing with continuous variables. Continuous variables have an infinite amount number of possibilities. They are the ones you have to round down. Since we're dealing with the longitude and latitude, these numbers have infinite possibilities.

Column J is a discrete variable because you can list all the numbers from 1-24. And unlike continuous variables, there are a definite amount of possibilities.

In this dataset, there seems to be a lot of missing information replaced by /N. In column J (Ward), they don't list the location of the ward. Only the number. Most people don't know what ward is where. So this is crucial information to input. 

In the same sense, I wonder how many of the resolved service requests have to do with their location and also the speed at which they're resolved.

## 3. Understanding Data

### 3.1. VIMO Analysis

I am using the VIMO analysis from the Data Accuracy and Validation: Methods to ensure the quality of the data by the Government of Canada (2022) to analyze the information in this dataset. 

For the first letter in the acronym, V, standing for Valid, the data should not be blank or missing and within a valid range. Looking at columns E and F, all the dates are within a realistic range. Since there is no date bigger than the current date. Like a year bigger than 2024.

In this dataset, there are several missing elements but with valid reasoning. This is due to there being public and private requests, where only the public requests are shown for the addresses (column G), latitude (column H) and longitude (column I). 

The second letter in the acronym, I, stands for invalid data. This means the data is an impossible outcome. For example, column J had a value of around -76 which is a longitude number. This is impossible for this column since the wards have to be from 1-24.

The third letter is M, which stands for missing values. In this dataset, it would be every instance where there's a \N. Most of the missing data is unknown for example the closed dates in column F. They're missing since the request is still active and has not yet been resolved.

The last letter, O, stands for outlier values, which are extremely small or extremely large results. Which sticks out of the dataset. This could mean it could be an error or invalid. But fortunately for us, there is no outlier value in this dataset.

### 3.2. Cleaning Data

1. The first tool I used to clean the data is the data cleaning suggestion tool in Google Sheets. This is found under Data, then by clicking data clean-up which leads to the clean-up suggestions. The only suggestion that popped up was to trim all the whitespaces. So by clicking the green checkmark, the system automatically implemented the changes.

![alt text](<Screenshot 2024-11-05 113708.png>)<br>
*Figure 4: The "Clean-up Suggestions" prompt on Google Sheets.*

2. I found that all the \N were distracting. So I decided to remove them by selecting all the columns and rows and then hitting "Edit". Then I hit on the find and replace function to replace \N with nothing.

![alt text](<Screenshot 2024-11-05 115727.png>)<br>
*Figure 5: The "Find and replace" function on Google Sheets for "\N".*

To be double safe, I replaced variant possibilities of the \N like /N. Which you can see here:

![alt text](<Screenshot 2024-11-05 115532.png>)<br>
*Figure 6: The "Find and replace" function on Google Sheets to replace "/N".*

3. Then, I wanted to ensure that everything was capitalized. So with every word in the dataset, I made sure to replace the uncapitalized version with the capitalzed version. As shown in this example:

![alt text](<Screenshot 2024-11-05 120314.png>)<br>
*Figure 7: The "Find and replace" function on Google Sheets for the word "Resolved".*

4. Then I also wanted to make sure there were no typos in the dataset. So if I noticed anything misspelled like "Cacelled" in Column B, I would change it to the proper form, in this case it would be "Cancelled". To do this, I used the find and replace tool to ensure that all the variants were changed. Like "ad" to "and" in column C, as seen here:

![alt text](<Screenshot 2024-11-05 120457.png>)<br>
*Figure 8: The "Find and replace" function on Google Sheets for "and".*

Then I manually fixed small typos in the titles like "Opeed" to "Opened" and "Descriptio" to "Description".

5. I do think that translations are important. But, it made this dataset look too busy. So by using the split text to columns tool in Google Sheets (found under Data). I split the English and French descriptions into two separate columns. 

First, I had to add an extra column to the right. Then hit on split text to columns and inputted the delimiter "|", since that's what was separating the French from English. Then I hit enter. The column was now split into two seperate columns. So I deleted the extra column containing French and repeated this process for column C (the type of requests). Those were the only columns containing French. 

I wanted to use the `SPLIT` function to complete this task but it was too inefficient to drag the function down to the bottom of the dataset. So this way was a lot more time efficient.

![alt text](<Screenshot 2024-11-05 124454.png>)<br>
*Figure 9: The "Split text to colums" function on Google Sheets.*

6. To finish up, I deleted all information I deemed unnecessary like the address, latitude, longitude and description columns. 

7. Then finally, I formatted it nicely by bolding, centering and colouring the titles. Then I formatted the body of texts to be either in the middle or on the left-hand side. 

After following these steps, this is what my cleaned dataset looks like:

![alt text](<Screenshot 2024-11-05 172601.png>)<br>
*Figure 10: The cleaned version of the 2024 Service Requests dataset.*

### 3.3. Exploratory Data Analysis (EDA)

To further explore this dataset and find a potential story. I chose to create a couple of pivot tables. The first one I made was for the frequency of methods used to call in service requests. I chose to do these two variables because when I was cleaning my data, I realized there were a lot of people using the web to ring in there requests as opposed to other forms of communication like in person for example. So already, I had an idea of what the results could be. I predicted that the web would take up a big portion of the total.

Here's my first pivot table:

![alt text](<Screenshot 2024-11-05 143041.png>)<br>
*Figure 11: Pivot table for the frequency of each Chanel counted by the Service Request ID.*

And the accompanying exploratory chart:

![alt text](<COUNTA of Service Request ID (1).png>)<br>
*Figure 12: Exploratory chart for the frequency of each Chanel counted by the Service Request ID .*

After creating the pivot table and exploratory chart, it is clear that I was right and the number of online web call-ins do stand out alongside dispatch. An interesting note is that the next biggest mode of communication is through the phone. And the smallest is Face2Face, meaning in person.

This can create a story of how people tend to do things more online nowadays. It means less commuting which is more efficient and convenient for them. So a potential story could be how our world has become more and more dependent on technology and turning online before anything else. And maybe even losing social interaction skills.

For my second pivot table, I wanted to figure out if the wards had something to do with the amount of service requests sent in. This was my initial thesis/question. But by taking a quick look at this data. Nothing stands out. Which doesn't make an interesting story. 

This is my second table:

![alt text](<Screenshot 2024-11-05 141012-1.png>)<br>
*Figure 13: Pivot table for the frequency of the ward counted by the Service Request ID.*

And the accompanying exploratory chart:

![alt text](<COUNTA of Service Request ID.png>)<br>
*Figure 14: Exploratory chart for the frequency of the ward counted by the Service Request ID.*

## 4. Potential Story

If I wanted to tell the story of how humans these days have turned to technology as a main source of communication. I could go in two different directions. The positive side or the negative side. In this case, I want to look at it through a more critical lens. On how this can impact us socially. How less and less human interactions affect us. Like how self-service cashiers and now robot servers are starting to become more mainstream. To do this, I could interview specialists in human psychology and ask them what the impacts on mental health are or can be when people have minimal interaction with other peoople. I would also need data on this topic to see if there's an increase in mental health issues or a link to anything else. 

After doing a bit of research, I found an answer to my questions. Written by Kendra Cherry on The Impact of Social Isolation on Mental Health (2023). She writes that "People are social creatures, and lacking support and contact with others can contribute to loneliness, cognitive decline, anxiety and depression."

So some follow-up questions would be: How would we fight this? Would it be possible to replicate human interaction? Maybe by using A.I.? "It is stated that 32% of people can’t tell the difference between AI and a human" (Press, 2023). This statistic was taken by the largest “Turing Test” with over 1.5 million participants (Press, 2023). And with the advancement of technology and focus on A.I, that number has probably doubled since then.

In all, this is definitely something worth looking into especially since this is the route we are going down as a society. This is the story I would chose to write about from this dataset using the pivot table and exploratory chart to aid with my point.

## 5. Conclusion

In conclusion, while doing this assignment, I found that cleaning the data was the hardest part. I feel like I wasted a lot of time trying to figure out how to properly use some of the tools. For example, I didn't know if you could manually give the `SPLIT` function a range. I also did a lot of find and replace to clean the data. Which became very time-consuming cause I had to rewrite every element in the dataset properly and the uncapitalized version as well. I assume that there is a more efficient way to do this since even after cleaning for hours, there still seemed to be invalid data in some of my columns that I didn't notice until I made some pivot tables.

The most rewarding part for me was finding the errors and making my dataset look clean enough to make a couple of pivot tables. Which then let me pull a narrative and form a clear story. When I was making the connections and links to other aspects of real life that was the most rewarding part for me. It was like I was using the dataset as evidence that more people lean towards doing things online nowadays. Creating a bigger picture using this dataset. 

A gap in my knowledge would have been the condensation of information. In one of my pivot tables, I had Walk-in and Face2face as two separate rows when they're essentially the same thing. And I find that I could have condensed even more information to make the dataset even cleaner.

## 6. References

Cherry, K. (2023). *The Impact of Social Isolation on Mental Health*. Verywell Mind. https://www.verywellmind.com/the-impact-of-social-isolation-on-mental-health-7185458

Government of Canada, S. C. (2021, September 2). *4 data exploration 4.2 types of variables. 4.2 Types of variables*. Government of Canada, Statistics Canada. https://www150.statcan.gc.ca/n1/edu/power-pouvoir/ch8/5214817-eng.htm

Government of Canada, S. C. (2022, May 11). *Data accuracy and validation: Methods to ensure the quality of data*. Government of Canada, Statistics Canada. https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/892000062020008

Press, G. (2023, June 01). *Is It An AI Chatbot Or A Human? 32% Can’t Tell*. Forbes. https://www.forbes.com/sites/gilpress/2023/06/01/is-it-an-ai-chatbot-or-a-human-32-cant-tell/