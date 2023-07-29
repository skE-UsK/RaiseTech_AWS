# [AWS::RDS::DBInstance](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-rds-dbinstance.html)


## 概要
Amazon RDS DB インスタンスを作成するための AWS CloudFormation リソースです。このリソースは、RDS DB インスタンスまたは Aurora DB クラスター内の DB インスタンスを作成することができます。

## プロパティの一覧
AllocatedStorage: ストレージ容量を指定する文字列です。  
AllowMajorVersionUpgrade: メジャーバージョンのアップグレードを許可するかどうかを指定するブール値です。  
AssociatedRoles: DBインスタンスに関連付けられたAWS Identity and Access Management（IAM）ロールのリストです。IAMロールは、DBインスタンスが他のAWSサービスにアクセスするための権限を付与します2。  
AutoMinorVersionUpgrade: マイナーバージョンの自動アップグレードを許可するかどうかを指定するブール値です。  
AvailabilityZone: DBインスタンスが配置されるアベイラビリティーゾーンを指定する文字列です。  

BackupRetentionPeriod: 自動バックアップの保持期間を指定する整数値です。  

CACertificateIdentifier: CA証明書識別子を指定する文字列です。  
CertificateDetails: 証明書の詳細を指定するCertificateDetailsオブジェクトです。  
CertificateRotationRestart: 証明書のローテーション時にDBインスタンスを再起動するかどうかを指定するブール値です。  
CharacterSetName: DBインスタンスで使用される文字セット名を指定する文字列です。  
CopyTagsToSnapshot: スナップショットにタグをコピーするかどうかを指定するブール値です。  
CustomIAMInstanceProfile: カスタムIAMインスタンスプロファイル名を指定する文字列です。  

DBClusterIdentifier: DBクラスターの識別子を指定する文字列です。  
DBClusterSnapshotIdentifier: DBクラスタースナップショットの識別子を指定する文字列です。  
DBInstanceClass: DBインスタンスクラスを指定する文字列です。  
DBInstanceIdentifier: DBインスタンスの識別子を指定する文字列です。  
DBName: データベース名を指定する文字列です。  
DBParameterGroupName: DBパラメーターグループ名を指定する文字列です。  
DBSecurityGroups: DBセキュリティグループのリストです。各セキュリティグループは、文字列で指定します。  
DBSnapshotIdentifier: DBスナップショットの識別子を指定する文字列です。  
DBSubnetGroupName: DBサブネットグループ名を指定する文字列です。  
DeleteAutomatedBackups: 自動バックアップを削除するかどうかを指定するブール値です。  
DeletionProtection: 削除保護を有効にするかどうかを指定するブール値です。  
Domain: ドメイン名を指定する文字列です。  
DomainIAMRoleName: ドメインIAMロール名を指定する文字列です。  

EnableCloudwatchLogsExports: Amazon CloudWatch Logs にエクスポートするログの種類を指定します。  
EnableIAMDatabaseAuthentication: IAM データベース認証を有効にするかどうかを指定します。  
EnablePerformanceInsights: Performance Insights を有効にするかどうかを指定します。  
Endpoint: DB インスタンスに接続するために必要な情報を表すデータ型です。  
Engine: DB インスタンスで使用するデータベースエンジンの種類を指定します。  
EngineVersion: DB インスタンスで使用するデータベースエンジンのバージョンを指定します。  

Iops: 入出力操作数を指定する整数値です。  

KmsKeyId: AWS Key Management Service（KMS）キーIDを指定する文字列です。  

LicenseModel: ライセンスモデルを指定する文字列です。  

ManageMasterUserPassword: マスターユーザーのパスワードを管理するかどうかを指定するブール値です。  
MasterUsername: マスターユーザー名を指定する文字列です。  
MasterUserPassword: マスターユーザーのパスワードを指定する文字列です。  
MasterUserSecret: マスターユーザーのシークレット情報を指定するMasterUserSecretオブジェクトです。  
MaxAllocatedStorage: 最大割り当てストレージ容量を指定する整数値です。  
MonitoringInterval: 監視間隔を指定する整数値です。  
MonitoringRoleArn: 監視ロールのARN（Amazon Resource Name）を指定する文字列です。  
MultiAZ: マルチAZデプロイメントを有効にするかどうかを指定するブール値です。  

NcharCharacterSetName: Oracle DB インスタンスで使用する NCHAR 文字セット名を指定します。  
NetworkType: DB インスタンスのネットワークタイプを指定します。  

OptionGroupName: DB インスタンスに関連付けるオプショングループ名を指定します。  

PerformanceInsightsKMSKeyId: Performance Insights データを暗号化するために使用する AWS KMS CMK の ID を指定します。  
PerformanceInsightsRetentionPeriod: Performance Insights データの保持期間（日数）を指定します。  
Port: DB インスタンスのポート番号を指定します。  
PreferredBackupWindow: DB インスタンスの自動バックアップウィンドウを指定します。  
PreferredMaintenanceWindow: DB インスタンスのメンテナンスウィンドウを指定します。  
ProcessorFeatures: DB インスタンスで使用するプロセッサー機能を指定します。  
PromotionTier: Aurora レプリカの昇格優先度を指定します。  
PubliclyAccessible: DB インスタンスがインターネットからアクセス可能かどうかを指定します。  

ReplicaMode: レプリカモードを指定する文字列です。　　
RestoreTime: 復元時刻を指定する文字列です。　　

SourceDBClusterIdentifier: ソースDBクラスターの識別子を指定する文字列です。　　
SourceDBInstanceAutomatedBackupsArn: ソースDBインスタンスの自動バックアップのARN（Amazon Resource Name）を指定する文字列です。　　
SourceDBInstanceIdentifier: ソースDBインスタンスの識別子を指定する文字列です。　　
SourceDbiResourceId: ソースDbiリソースIDを指定する文字列です。　　
SourceRegion: ソースリージョンを指定する文字列です。　　
StorageEncrypted: ストレージ暗号化を有効にするかどうかを指定するブール値です。　　
StorageThroughput: ストレージスループットを指定する整数値です。　　
StorageType: ストレージタイプを指定する文字列です。　　

Tags: DB インスタンスに関連付けるタグを指定します。　　
Timezone: Microsoft SQL Server DB インスタンスで使用するタイムゾーンを指定します。　　

UseDefaultProcessorFeatures: DB インスタンスでデフォルトのプロセッサー機能を使用するかどうかを指定します。　　
UseLatestRestorableTime: DB スナップショットから DB インスタンスを復元する場合、最新の復元可能な時刻を使用するかどうかを指定します。　　

VPCSecurityGroups: DB インスタンスに関連付ける VPC セキュリティグループの ID を指定します。
