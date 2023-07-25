# [AWS::EC2::KeyPair](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-keypair.html)

## 概要
Amazon Elastic Compute Cloud (EC2) インスタンスで使用するキーペアを指定します。既存のキーペアをインポートするには、PublicKeyMaterial プロパティを含めます。新しいキーペアを作成するには、PublicKeyMaterial プロパティを省略します。既存のキーペアをインポートする場合、キーの公開鍵マテリアルを指定します。

## プロパティの一覧
KeyFormat: キーペアの形式。デフォルト: pem。必須: いいえ。タイプ: 文字列。許可される値: pem | ppk。更新には置換が必要です。  
KeyName: キーペアの一意の名前。制約: 最大255文字のASCII文字。必須: はい。タイプ: 文字列。  
KeyType: キーペアのタイプ。ED25519 キーは Windows インスタンスではサポートされていないことに注意してください。  
プロパティが指定されている場合PublicKeyMaterial、KeyTypeプロパティは無視され、キーのタイプはPublicKeyMaterial値から推測されます。デフォルト：rsa

PublicKeyMaterial: 既存のキーペアをインポートする場合、キーの公開鍵マテリアルを指定します。

Tags: AWS リソースに割り当てるタグのリスト。