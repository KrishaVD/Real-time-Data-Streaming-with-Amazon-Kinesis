# Real-time-Data-Streaming-with-Amazon-Kinesis

If you are looking to get started with real-time data streaming and processing using Amazon Kinesis, you're in the right place. This beginner-friendly guide will walk you through creating a simple project to understand the basics of Amazon Kinesis.

# Prerequisites
-	An AWS account
-	Basic knowledge of Python
-	Visual Studio Code installed
-	AWS CLI configured with appropriate permissions
  
# Step 1: Create a Kinesis Data Stream
Go to the AWS Management Console, navigate to Kinesis under "Services". Click on "Create Data Stream", enter a name for your stream, and choose the number of shards (starting with 1 is fine). Click on "Create".

# Step 2: Create a Kinesis Data Firehose Delivery Stream
-	In Kinesis Dashboard, select "Delivery streams" from the left sidebar.
-	Click on "Create delivery stream".
-	Name your delivery stream and under "Source", select "Kinesis stream" and choose the stream created earlier.
-	In "Process records", choose "Disabled".
-	For "Destination", select "Amazon S3" and pick an S3 bucket to store the processed data.
-	Finish by clicking "Create delivery stream".

# Step 3: Create a Python Script to Send Data to Kinesis Stream
-	Open Visual Studio Code.
-	Create a new file with a `.py` extension, for example, `send_data.py`.
-	Write the following Python script in the file:

```python
import boto3
import json
import random

# Initialize a Kinesis client
kinesis = boto3.client('kinesis')

# Name of your Kinesis data stream
stream_name = 'YourDataStreamName'

# Replace this with the logic for fetching your data
# Example:
# data = fetch_data_from_api()

# Send the data to the Kinesis stream
kinesis.put_record(
    StreamName=stream_name,
    Data=json.dumps(data),
    PartitionKey=str(random.randrange(10000))
)
```

-	Save the file.

Running the Script
-	Open Command Prompt.
-	Navigate to the directory where your script is located using the `cd` command.
-	Run the script using Python by executing `python send_data.py`.

# Step 4: Process Streaming Data with Kinesis Data Analytics
-	Go back to Kinesis Dashboard, select "Data Analytics" from the left sidebar.
-	Click on "Create Analytics Application".
-	Name your application, and under "Source", choose the Kinesis stream you created earlier.
-	You can now use SQL queries to process the data in real-time. For example, to filter out records of users aged more than 21, use: `SELECT * FROM your_stream_name WHERE age > 21;`.
-	For "Destination", choose the Kinesis Firehose delivery stream created earlier.

# Step 5: Monitor Your S3 Bucket
-	Go to the S3 service in the AWS Management Console.
-	Open the bucket selected as the destination in Kinesis Data Firehose.
-	You should start seeing the processed data stored in this bucket in near real-time.


# Conclusion
Congratulations! You've successfully set up a real-time data streaming and processing pipeline using Amazon Kinesis. This guide should help you get started with Kinesis and its capabilities. Feel free to experiment and try out different data sources and processing logic as you become more comfortable with the service.
