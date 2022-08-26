# Perx Data Interview-1 :: Data Intern

## A) SQL Test

### Prerequisite:

* Redshift (https://aws.amazon.com/redshift/free-trial/)
* Required CSV files are in folder `.Data-intern/Sample-data`, import into Redshift in three diffrent tables as mentioned below. (Redshift's free trial should be enough for this exercise)

* Table and Relation:
 1.  Campaign (id , name , updated_at)
 2.  Reward_campaigns( id , Reward_name , updated_at, campaign_id(FK(campaign.id)))
 3.  Reward_transactions(id, status, updated_at, Reward_camapigns_id(FK(Reward_camapigns.id)) )

### Use Case 1:

Client X would like to identify the most popular engagement day and time between a specific date range (Database stored data is in UTC format and input will be in SGT) for a Campaign.
 
   * Expected Output:
           No Of Transaction | Date | Time 

### Use Case 2:
         
Client X would like to see the weekly breakdown of reward performance along with comparison of previous week.

   * Expected Output:
          Reward name | Reward Redeemed count | Percentage difference as per previous week | Date/ Week 

### Deliverable

SQLs with output.