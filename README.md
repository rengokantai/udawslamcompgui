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
