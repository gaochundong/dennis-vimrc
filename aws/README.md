
```bash
# 命令行从 AWS Dynamodb 表读取数据，JSON格式，解析JSON读取需要的字段，导出csv，中文转码，生成文件
aws --profile saml --region cn-north-1 dynamodb scan --table-name DUMMY_TABLE --output json --query "Items[*].[c1.S,c2.S,c3.S,c4.BOOL,c5.S,c6.M.level.S,c6.M.events.L[0].S]" | jq -r '.[] | @csv' | iconv -f UTF8 -t GB18030 > ~/g/tmp/items.csv

# 命令行申请 STS 临时 Token
aws sts assume-role-with-web-identity --role-arn arn:aws-cn:iam::ACCOUNT_ID:role/ROLE_NAME --role-session-name SESSION_NAME --duration-seconds 1000 --web-identity-token file://token.txt --region cn-north-1 | jq
```
