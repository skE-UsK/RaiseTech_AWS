# [AWS::IAM::InstanceProfile](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-iam-instanceprofile.html)

## 概要
IAMインスタンスプロファイルは、Amazon EC2インスタンスにIAMロールを割り当てるために使用されます。

## プロパティの一覧
InstanceProfileName: インスタンスプロファイルの名前。この名前は、AWSアカウント内で一意である必要があります。

Path: インスタンスプロファイルのパス。この値は、IAMリソースを組織化するために使用されます。

Roles: インスタンスプロファイルに関連付けるIAMロールのリスト。このリストには、1つのIAMロールのみを指定できます。
