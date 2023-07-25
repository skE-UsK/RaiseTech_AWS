# [AWS::KMS::Key](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-kms-key.html)

## 概要
WS Key Management Service (AWS KMS)のキーを表します。AWS KMSは、データ暗号化に使用される暗号化キーを簡単に作成および管理できるサービスです。

## プロパティの一覧
Description: キーに関する説明を指定します。  

Enabled: キーが有効かどうかを指定します。  
EnableKeyRotation: キーの自動ローテーションを有効にするかどうかを指定します。  

KeyPolicy: キーのポリシーを指定します。  
KeySpec: キーの仕様を指定します。対称暗号化キーの場合、SYMMETRIC_DEFAULTを指定します。  
KeyUsage: キーの使用方法を指定します。対称暗号化キーの場合、ENCRYPT_DECRYPTを指定します。  

MultiRegion: マルチリージョンキーかどうかを指定します。  

PendingWindowInDays: キー削除の保留期間（日数）を指定します。  

Tags: キーにタグを付けることができます。  