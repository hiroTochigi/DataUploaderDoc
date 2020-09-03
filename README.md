# Data Uploader

## What Data Uploader does?

Upload local Excel/CSV file on an existing Monday board

Data type is limited. Data Uploader can upload the following data type
1. Name
1. Text
1. Number
1. Date
1. Label
1. Long-text

## How to use it

### Prerequisites 
First of all, You must run this application on [Monday.com](https://monday.com/)
Second, Data Uploader is designed to run on [Widget](https://support.monday.com/hc/en-us/articles/360007078739-The-Overview-Widget).

### How to install it
You can bring Data Uploader to your Monday account from [this link](https://auth.monday.com/oauth2/authorize?client_id=c083411c8ecb1a8cadbf3a0f493b5e12&response_type=install)

Also, you can build and try to test Data Uploader in local environment.
In the case, you must have node(v10.22.0 or above) and npm(6.14.6 or above)
Please look at [this page](https://monday.com/developers/apps/intro) to run on this application on your account.

### Configuration
Before running Data Uploader, you must configure Data Uploader.

You must have Configuration board
![img1](https://raw.githubusercontent.com/hiroTochigi/Data-Uploader/master/images/Data%20Uploader.png)


This is an example of Configuration board.
![img2](https://raw.githubusercontent.com/hiroTochigi/Data-Uploader/master/images/Configuration.png)
1. Group name must be a name of a target board.
1. The first column must be local Excel/CSV file headers
1. `Monday` column must be column headers in the target Board
1. `Is ID?` column indicates which column should be identifier. Data Uploader compares values of this column to identify each item on both data set. In the above example, Request and Name are the IDs.
1. `Exclusive Labels` column informs Data Uploader what Label value should not be changed. In the above example, If `Status` column on Marketing board has value `Stuck` or `On hold`, Data Uploader does not change `Status` column whatever the local data set has in `Status` column. (Only works on Label type)
1. `Criteria` column informs Data Uploader updating criteria.`Criteria` must have `,==` or `,!=` after a label value. In the above example, if some rows in the local data set has `Status` column having value `Completed`, Data Uploader does not update the rows on Monday board. If `Criteria` column in Status row has `Done,==`, only items with `Status` value having `Done` are uploaded (Only works on Label).


The below is the example of Configuration board, a local data set, and a target board
![img3](https://raw.githubusercontent.com/hiroTochigi/Data-Uploader/master/images/Configuration2.PNG)


## Inspiration
We use an ERP to manage our daily jobs, but the ERP is very poor to present job flows.

[Monday.com](https://monday.com/) can visualize job flows clearly and let users share information easiliy. 

In addition, Monday has awesome integration and automation functions to make daily routine jobs easier and more efficient.

Monday.com allows users to upload Excel file to initiate Board.

However, users have to upload new data on their existing board manually.

In our use case, it is a serious bottleneck.

Sometimes, we have to upload a few dozens jobs in a day.

The intense manual data entry task is not only to waste our colleagues' productive time but also cause data integrity problem which might induce serious problems.

This application can take Excel file and update items via Monday GraphQL API.

User can specify id on Monday board data and local Excel data, so this app choose new data from Excel file and upload them.

This app releases our colleagues from their tedious data entry tasks and provides error free data entry services.

## What it does
Data Uploader takes local Excel file and update Monday board.
This application compares the local data and the data on the Monday board, and if the program detects difference, add new items or update the existing in the Monday board.
This application can update the following columns: name, text, number, date, long-text, and label.

## How I built it
I built it with React.js

## Challenges I ran into
Generating GraphQL query according to the data type.
Transforming Excel/CSV Data format into JavaScript Data format. 
Coming up with the data structure to compare two data sets.
Asynchronous function calls 

## Accomplishments that I'm proud of
Generating configuration data from Configuration variables.

## What I learned
JavaScript, mainly how to use Promise Object and functional programming paradigm
React.js

## What's next for Data Uploader
Prevent the users from making the wrong configuration file.
Almost all errors are generated because of the incorrect configuration file or the wrong data in the local data set, such as a number column having text and a label column having a nonexistent label.

1. Add a GUI configuration file generator to prevent typos.
1. Add a more user friendly error handling method, such as before generating a query, scan each local column data and warning users of the potential problem.
1. Add a history mode: reverse the uploading event.



