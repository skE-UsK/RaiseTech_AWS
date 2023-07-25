# [AWS::RDS::DBSecurityGroup](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-properties-rds-security-group.html)

## 概要
Amazon RDS DBセキュリティグループを作成または更新するAWS CloudFormationリソースです。ただし、DBセキュリティグループはEC2-Classicプラットフォームの一部であり、すべてのリージョンでサポートされているわけではありません。そのようなリージョンでは、代わりに AWS::EC2::SecurityGroup リソースを使用することが推奨されます。

## プロパティの一覧
DBSecurityGroupIngress: このプロパティは、DBセキュリティグループへのイングレスを指定するために使用されます。Ingress 型のリストが必要です。

EC2VpcId: このプロパティは、DBセキュリティグループが関連付けられるAmazon VPCのIDを指定します。文字列値が必要です。

GroupDescription: このプロパティは、DBセキュリティグループの説明を指定します。文字列値が必要です。

Tags: このプロパティは、DBセキュリティグループに関連付けるタグのリストを指定します。Tag 型のリストが必要です。