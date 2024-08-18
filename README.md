# Sales Data Projection 
## Objective
- Create a near real-time CDC pipeline such that the changes (insertion, updation, deletion) are consumed and ingested into S3 so that analysis can be done.
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
- `Sales-Data-Projection`/
  - `img`/
  - `data_generator.py`
  - `transformation_layer_with_lambda.py`

