# Near Real Time CDC Pipeline
## Objective
- Create a near real-time CDC pipeline such that the changes (insertion, updation, deletion) are consumed and dumped into S3 so that analysis can be done.
## Data 
- Mock sales data with columns orderid, product_name, quantity, price
## Cloud Service
- AWS
## Techstacks
- DynamoDB
- DynamoDB stream (for CDC)
- Kinesis stream
- Kinesis Firehose (for batch streaming data)
- Eventbridge Pipe (for stream ingestion)
- Lambda function (for transformation)
- Athena (for analysis)
- S3 (destination)
## Architecture 
<img src="https://github.com/sandeepdevamisra/Sales-Data-Projection/blob/main/img/architecture.png" alt="architecture" width="100%">

## File structure
- `Near-Real-Time-CDC-Pipeline`/
  - `img`/
  - `data_generator.py`
  - `transformation_layer_with_lambda.py`

## Steps
- Create a bucket in S3 (data will land here).
- Create a DynamoDB table with orderID as the partition key.
- Enable DynamoDB stream and select new image. This will let us do the CDC.
- Setup a Kinesis stream.
- Setup a EventBridge Pipe with source as DynamoDB stream, and target as Kinesis stream with partition key as eventID. We will not use the filtering and enrichment part. 
- Create a Kinesis Firehose for batching this real-time stream to mini-batches. Source is Kinesis datastream and destination is S3.
- Transform the data coming to Firehose before sending to S3 using a [lambda function](https://github.com/sandeepdevamisra/Near-Real-Time-CDC-Pipeline/blob/main/transformation_layer_with_lambda.py). Data will be ingested as JSON in S3.
- Make necessary transformations such that data is well-formatted.
- For querying it using Athena, use Glue crawler on S3.

## Run instructions
- Run the command `python3 data_generator.py` from terminal and the data will be continously ingested in the DynamoDB table. After some time, the data will be present in S3 and if we do any changes in the records in the table, the changed values will be captured and dumped in S3. 
