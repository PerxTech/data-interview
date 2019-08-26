# Perx Data Interview

## A) SQL Test

### Prerequisite:

* BigQuery Account.
* Attached CSV files having related data,import into BigQuery in three diffrent table as mentioned below.    
* Table and Relation:
 1.  Campaign (id , name , updated_at)
 2.  Reward_camapigns( id , Reward_name , updated_at, campaign_id(FK(campaign.id)))
 3.  Reward_transactions(id, status, updated_at, Reward_camapigns_id(FK(Reward_camapigns.id)) )

 ### 1. Use Case: 

  Client X whould like to find the most popular engagement day and time between specific date range (Database stored data is in UTC format and input will be in SGT) for a Campaign
 
   * Expected Output:
           No Of Transaction | Date | Time 

### 2. Use Case:
         
 Client X would like to see the reward performance weekly breakdown along with comparison of previous week.

   * Expected Output:
          Reward name | reward Redeemed count | Percentage difference as per previous week | Date/ Week 

## B) Analyse HTTP Log for User Sessions

### Use Case

Client X would like to find out the campaign performance for a certain time frame from HTTP log.

A campaign may results in http requests including:

* GET request to `/campaign/{{id}}`
* POST request to `/reward/{{id}}` (get a reward issued to the user)

A session window for a user is defined as: within which there's activity for a user (http request for the user) and gap between each activity is less than 5 mins.

Need to provide a report that has following fieds:

* user_id
* session_start (timestamp)
* session_end (timestamp)
* campaigns: list of campaigns the user viewd
* rewards_issued: list of rewards the user got issued
* reward_driven_by_campaign_view: true if user got a reward issued after viewing a campaign that contains the reward within the session

### Tasks

1. Create an avro schema for the HTTP log and convert the http log data provided to avro format
2. Load the avro data into a bigquery table
3. Load the campaign and reward mapping csv into a bigquery table
4. Do the processing to create the result

#### Data Provided

HTTP log is provided as text file with each line as one entry. Fields in the log entry are delimited by space with following format:

```
timestamp http_method http_path user_id
```

The following list describes the fields of an access log entry.

* timestamp: iso8601 timestamp (exmaple: `2019-06-01T18:00:00.829+08:00`)
* http_method
* http_path: The http request path
* user_id: User identifier

Mapping of campaign and reward is provided as a csv file.

Campaign and reward is one to many relationship.

### Deliverable

The avro schema need to be created manually as avsc file. All other tasks need to be encapsulated in a jupyter notebook and shared via a private github repo.

Inside the jupyter notebook, it's free to use any python library.

Even though the provided dataset is small, writing code that can accommodate very large dataset is preferred. Using frameworks like apache beam is encouraged.

## C) Machine Learning for Recommendation Task

### Use Case

Client X would like to understand its customers behaviour to recommend relevant rewards for future campaigns.

### Specification

Create a working machine learning (unsupervised model) solution that recommend rewards when input a user_id.

You are free to use any framework including tensorflow, teras, scikit-learn and pytorch.

### Data Provided

Please use the public [movielens 1M dataset](https://grouplens.org/datasets/movielens/1m)

### Deliverable

A command line application that can be invoked with user_id as parameter and output recommended movie ids. Or even better a simple rest service that packaged as docker image that expose a simple rest API that returns recommended movie ids for a user specified.
