#### udawslamcompgui

- cp2
```
aws lambda list-functions
```
- cp3
create a new role, attach awslambdaexecute,next step

copy this line: ```arn:aws:iam::6441268679:role/executionrole```
create a text 
```
{
 "key1":"value1",
"key2":"value2"
}
```

upload function:
```
aws lambda create-function --region us-west-2 --function-name ke --zip-file fileb://ke.zip --role arn:aws:iam::6441268679:role/executionrole --handler ke.handler --runtime nodejs --debug 
```
invoke function:(here, use a txt file)
```
aws lambda invoke-async --function ke --invoke-args test.txt --debug
```
update function:
```
aws lambda update-function-code --region us-west-2 --function-name ke --zip-file fileb://ke.zip
```
get paticular function name
```
aws lambda get-function --function-name ke
```
delete function name
```
aws lambda delete-function --function-name ke
```

==
- cp4
```
aws lambda create-function --region us-west-2 --function-name thumb --zip-file fileb://thumb.zip --role arn:aws:iam::6441268679:role/executionrole --handler thumb.handler --runtime nodejs --timeout 10 --memory-size 1024 --debug 
```

- cp5
lambda cmd:
```
aws lambda create-function --region us-west-2 --function-name kinesis --zip-file fileb://kinesis.zip --role arn:aws:iam::644126867916:role/kinesisrole --handler kinesis.handler --runtime nodejs --debug
```
invoke:
```
aws lambda invoke-async --function kinesis --invoke-args kinesis.txt --debug
```
create stream: (maunally test)
```
aws kinesis create-stream --stream-name kinesisstream --shard-count 1
aws kinesis describe-stream --stream-name kinesisstream  //get stream arn
```
create event source mapping
```
aws lambda create-event-source-mapping --function-name kinesis --event-source arn:aws:kinesis:us-west-2:644126867916:stream/kinesisstream --batch-size 100 --starting-position TRIM_HORIZON
```
then
```
aws kinesis put-record --stream-name kinesisstream --data "ke test" --partition-key ke  (shardId-000000000000)
```
