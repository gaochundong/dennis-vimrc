
```bash
# 命令行解析 JWT Token
echo eyJhbGciOiJIUzUxMiJ9.eyJpZGVudGl0eUlkIjoibnVsbEA4NjMzNDYwMzk5MDMwMDMiLCJleHAiOjE1ODU4MTkzOTAsImlhdCI6MTU4NTgxNTc5MH0.fwEpcVkvhG3-Z5cdY3-g_n20kgumNkPC9rUBQBAnj9cvjHYLUQYCKzGH6Ip163HRJ-FkuJU4-u5l8UVfFNzWMw | jq -R 'split(".") | .[1] | @base64d | fromjson'

# 命令行解析 JWT Token
cat token.txt | jq -R 'split(".") | .[1] | @base64d | fromjson'

# 命令行从 AWS Dynamodb 表读取数据，JSON格式，解析JSON读取需要的字段，导出csv，中文转码，生成文件
aws --profile saml --region cn-north-1 dynamodb scan --table-name DUMMY_TABLE --output json --query "Items[*].[c1.S,c2.S,c3.S,c4.BOOL,c5.S,c6.M.level.S,c6.M.events.L[0].S]" | jq -r '.[] | @csv' | iconv -f UTF8 -t GB18030 > ~/g/tmp/items.csv
```
