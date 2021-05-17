# The Lab Scenario
## Context
Imagine you are a systems administrator in charge of the health of a large web server cluster. As part of your duties you need to constantly monitor the server access logs for anything out of the ordinary. Normally you would have sent these logs to a log server and parsed the data with your nifty scripting skills. However the cluster has grown exponentially large within the last few months and now requires something more robust to keep up with the demand. You are tasked with creating a Log Analytics solution that is extremely scalable within AWS. 

In this lab you will produce data with the Kinesis Agent running on an EC2 instance. This will simulate one of the web servers in our very large farm. Then you will ingest some dummy access logs with Kinesis Data Streams. Move those to S3 and set the bucket lifecycle policy. Then you will have Kinesis Analytics get data, aggregate data points that Kinesis Analytics will output. Finally you will send the aggregated data to another Kinesis Firehose that outputs the data to Amazon Elasticsearch Service, which will then be visualized with Kibana. Here is a basic schematic of what you will be doing. 

![image](https://user-images.githubusercontent.com/4485129/118531801-dcdc4300-b763-11eb-946f-95cc6f0af1cf.png)


💁‍♂ Ok, best of luck with this lab. If you get stuck, head over to the forums.

 

## Accessing the AWS Management Console
At the top of these instructions, click Start Lab to launch your lab.

1. A Start Lab panel opens displaying the lab status.
* Wait until you see the message "Lab status: ready", then click the X to close the Start Lab panel.
* At the top of these instructions, click AWS
* This will open the AWS Management Console in a new browser tab. The system will automatically log you in.    

     **TIP:** If a new browser tab does not open, there will typically be a banner or icon at the top of your browser indicating that your browser is preventing the site from opening pop-up windows. Click on the banner or icon and choose "Allow pop ups."

Arrange the AWS Management Console tab so that it displays along side these instructions. Ideally, you will be able to see both browser tabs at the same time, to make it easier to follow the lab steps.

 

## Lab Steps
### Stage 1 - Creating an Amazon ElasticSearch Service Cluster
In this section you will use a FMI or Fill Me In.  They will be designated by . Make sure to remove the <> when entering them. 

1. Choose Services and search for Elasticsearch Service. Choose Create a new domain.  Choose Development and testing. Choose 7.9 as the Elasticsearch version. Choose Next. Paste the following for Elasticsearch domain name:

      web-log-summary
      
Leave the remaining settings as the defaults. Choose Next.  

2. Choose Public access under Network configuration. Keep in mind for a production level workload you would want this in a VPC, but for testing purposes we will use Public access. A production cluster can have more restrictive policies including restricting IP addresses or hosting the cluster in a private subnet.

3. Choose Create master user.  Use the following information for the username and password:

Master username:
      admin

Master password:
      #MasterPassword1@
      
Confirm master password:
      #MasterPassword1@
      
4. For Domain access policy choose JSON defined access policy and paste in the following:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "*"
        ]
      },
      "Action": [
        "es:*"
      ],
      "Resource": "arn:aws:es:us-east-1:<FMI>:domain/web-log-summary/*"
    }
  ]
}
```
Replace the  in the above JSON with the actual account number at the top right next to the Region which should be N. Virginia.  It should have a format similar to 0000-0000-0000.  Remove the dashes and replace the  for example:

```
      ],
      "Resource": "arn:aws:es:us-east-1:000000000000:domain/web-log-summary/*"
    }
```

5. Choose Next. Choose Confirm.  This will take about 10-15 minutes to complete.

We will move on to creating the Kinesis firehose while we wait for the ES cluster to complete. 

In this section you will use a FMI or Fill Me In.  They will be designated by . Make sure to remove the <> when entering them. 

### Stage 2 - Create a Kinesis stream and Amazon S3 Bucket
1. Choose Services and search for Kinesis.  Choose Kinesis Data Firehose which will be our delivery stream.  

2. Choose Create delivery stream. For the Delivery stream name paste in:
      web-log-ingestion-stream

Leave everything else as the defaults and choose Next.    
Again on the Process records page leave everything as the default and choose Next.   

3. On the Choose a destination page leave Amazon S3 as the Destination. Scroll down and choose Create new next to Choose a bucket.   

4. Give the S3 bucket name a unique name such as your initials:
      <FMI>-web-log-ingestion-bucket
  
Example:
      emr-web-log-ingestion-bucket

Leave the Region as US East (N. Virginia) as this is where our ES cluster and Kinesis streams will live.

5. Choose Create S3 bucket. Leave everything else as the default and choose Next.  
6. Under S3 buffer conditions change the Buffer size to 1, and the Buffer interval to 60.
7. Leave the rest as the default and choose Next.  Finally choose Create delivery stream. Wait until the Status shows as Active before moving on to Stage 3.  
In this next section you will install the Kinesis Agent onto the EC2 instance. For this example there is a python script that runs in the background which is what is generating our server access logs. Feel free to take a look at the access logs in the /tmp/logs directory. 

### Stage 3 - Installing the Kinesis Agent

1. Choose Services and search for EC2. Choose Instances (running).
2. There should be a Dummy Web Server instance already running. Choose the Instance ID to open the instance summary information.
3. Choose Connect. Verify Session Manager is selected and choose Connect. This will load a session and you should be presented with a shell prompt: sh-4.2$.
4. You will now need to install the Kinesis agent onto the instance.  In the session run the following:

      sudo yum install –y aws-kinesis-agent
Then you will need to edit the agent.json and add in the deliveryStream with the Kinesis Firehose which was created in Stage 2. 

Open up following file /etc/aws-kinesis/agent.json file in your favorite text editor.  For this example we will use VI:

sudo vim /etc/aws-kinesis/agent.json
Replace the current contents of agent.json which should look like this:
```
{
  "cloudwatch.emitMetrics": true,
  "kinesis.endpoint": "",
  "firehose.endpoint": "",
​
  "flows": [
    {
      "filePattern": "/tmp/app.log*",
      "kinesisStream": "yourkinesisstream",
      "partitionKeyOption": "RANDOM"
    },
    {
      "filePattern": "/tmp/app.log*",
      "deliveryStream": "yourdeliverystream"
    }
  ]
}
```
With this:
```
{
        "cloudwatch.emitMetrics": true,
        "kinesis.endpoint": "",
        "firehose.endpoint": "",
        "flows": [{
                "filePattern": "/tmp/logs/access_log*",
                "deliveryStream": "<FMI>",
                "dataProcessingOptions": [{
                        "optionName": "LOGTOJSON",
                        "logFormat": "COMMONAPACHELOG"
                }]
        }]
}
```
You will need to use your deliveryStream in place of the  which should be web-log-ingestion-stream.

If you decided to name it something else you can get the name by running the following:

aws firehose list-delivery-streams --region us-east-1
```
{
    "DeliveryStreamNames": [
        "web-log-ingestion-stream"
    ],
    "HasMoreDeliveryStreams": false
}
```

Ultimately the final file should look like the following:

```
{
        "cloudwatch.emitMetrics": true,
        "kinesis.endpoint": "",
        "firehose.endpoint": "",
        "flows": [{
                "filePattern": "/tmp/logs/access_log*",
                "deliveryStream": "web-log-ingestion-stream",
                "dataProcessingOptions": [{
                        "optionName": "LOGTOJSON",
                        "logFormat": "COMMONAPACHELOG"
                }]
        }]
}

```
Save the file.  

Now to start the agent.  Run the following command to start the Kinesis agent:

sudo service aws-kinesis-agent start
You can look at the /var/log/aws-kinesis-agent/aws-kinesis-agent.log if you want to see exactly what is happening. Keep in mind it can take around 5 minutes before data starts to appear in your Kinesis Firehose. 

In this next section you will create the second Kinesis Firehose. This Firehose will dump the data to Amazon ElasticSearch. 

### Stage 4 - Creating the second Kinesis Firehose
Switch back to the EC2 tab. Choose Services and Kinesis. Under Data Firehose choose Create delivery stream. 

For Delivery stream name paste in the following:

web-log-aggregated-data
Choose Next. On the Process records page choose Next. 

Choose Amazon Elasticsearch. Then under Domain choose the ES domain that was set up in Stage 1. Which should be web-log-summary. If it's grey and says "Processing", choose the refresh button next to it. Then choose it. If it's still grey and "Processing" it may still be creating. Grab a coffee or tea and wait a bit then refresh again. 

For Index paste in request_data.

Under S3 backup leave Failed records only selected.  Next to Choose a bucket choose Create new. For the S3 bucket name again use your initials + web-log-aggregated-errors:

<FMI>-web-log-aggregated-errors
Example:

emr-web-log-aggregated-errors
Leave the Region as US East (N. Virginia) and choose Create S3 bucket.

Choose Next. Under S3 buffer conditions change the Buffer size to 1, and the Buffer interval to 60.

Choose Next.

Choose Create delivery stream. Wait for the Status to become Active.

Choose Services and IAM. Choose Roles and search for KinesisFirehoseServiceRole-web-log-aggre. Copy the Role ARN value which should look similar to the following:

arn:aws:iam::000000000000:role/service-role/KinesisFirehoseServiceRole-web-log-aggre-us-east-1-0000000000000
Choose Services and Elasticsearch Service. Choose web-log-summary under Domain. Choose the link next to Kibana. This will launch the Kibana dashboard. Login with our ES information:

username: admin
​
password: #MasterPassword1@
Expand the sidebar by choosing the icon on Kibana's upper left corner, choose Security.

Choose Roles in the sidebar.

Search for the all_access role and choose it. 

Choose the Mapped users tab. 

Choose Manage mapping. 

In the Users box, paste the IAM Role ARN which again should look similar to the following:

arn:aws:iam::000000000000:role/service-role/KinesisFirehoseServiceRole-web-log-aggre-us-east-1-0000000000000
Press Enter after pasting and choose Map. You should have an admin user and a user with the ARN that was just copied.

### Stage 5 - Creating the Kinesis Analytics Application

Switch back to the AWS tab. Choose Services and Kinesis. Under Data Analytics choose Create application. 

For the Application name paste in the following:

web-log-aggregation-app
Leave SQL selected and choose Create application.

Choose Connect streaming data. Under Source choose Kinesis Firehose delivery stream. Choose the web-log-ingestion-stream. 

Choose Discovery schema and wait for the schema to populate. Choose Save and continue. 

Choose Go to SQL editor. Choose Yes, start application. After about 30-90 seconds the application should start.

Remove everything in the SQL editor and paste in the following:
```
CREATE OR REPLACE STREAM "DESTINATION_SQL_STREAM"
  (datetime TIMESTAMP, status INTEGER, statusCount INTEGER);
​
CREATE OR REPLACE PUMP "STREAM_PUMP" AS INSERT INTO "DESTINATION_SQL_STREAM"
SELECT STREAM ROWTIME as datetime, "response" as status, COUNT(*) AS statusCount
FROM "SOURCE_SQL_STREAM_001"
GROUP BY "response",
FLOOR(("SOURCE_SQL_STREAM_001".ROWTIME - TIMESTAMP '1970-01-01 00:00:00') minute / 1 TO MINUTE);
```
Choose Save and run SQL. 

Choose Destination. Choose Connect to a destination. 

Under Destination choose Kinesis Firehose delivery stream and choose web-log-aggregated-data from the drop down.

Leave Choose an existing in-application stream selected.

Under In-application stream name choose DESTINATION_SQL_STREAM from the drop down.

Choose Save and continue.

Choose Exit to Kinesis Data Analytics applications. 

### Stage 6 - Visualize data in Kibana
Switch back to the Kibana tab. Choose the Visualize icon on the left hand toolbar. 
Choose Create index pattern. Paste the following into Index pattern: request_data. 
Choose Next step. Choose Create index pattern. Choose the Visualize icon again on the left hand toolbar.
Choose Create new visualization. Choose the Pie. Choose request_data.
For Metrics choose Slice size Count. Under Aggregation choose Sum.
Under Field choose STATUSCOUNT. 
Under Buckets choose Add. Choose Split slices. Under Aggregation chose Terms. Under Field choose STATUS. 
Choose Update. 
The Pie chart should now show the number of requests based on the status codes. 
Notice that in this solution, we are using Kinesis to ingest the raw data and saving into S3, and only a refined version of the data gets into Amazon Elasticsearch Service. Depending on how you want to architect your data lake solution and taking many other subjects into consideration (budget included), you may want to send your raw logs straight out to Elasticsearch and do all that filtering in Kibana. The way you design your solution is up to you and remember, it is all regarding matching the workload to the necessity!

## Ending the lab
At the top of these instructions, click End Lab.
A pop up will ask you to confirm this.  choose Yes.  
