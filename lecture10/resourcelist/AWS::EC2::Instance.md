# [AWS::EC2::Instance](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html)

## 概要
EC2インスタンスが作成されます。

## プロパティの一覧
AdditionalInfo: インスタンスに関する追加情報を指定します。  
Affinity: インスタンスと専用ホストとの親和性を指定します。  
AvailabilityZone: インスタンスが作成されるアベイラビリティーゾーンを指定します。

BlockDeviceMappings: インスタンスに接続するブロックデバイスのマッピングを指定します。  

CpuOptions: インスタンスのCPUオプションを指定します。  
CreditSpecification: T2またはT3インスタンスのCPUクレジットオプションを指定します。  

DisableApiTermination: インスタンスのAPI終了を無効にするかどうかを指定します。  

EbsOptimized: インスタンスがEBS最適化されているかどうかを指定します。  
ElasticGpuSpecifications: インスタンスに接続するElastic GPUの仕様を指定します。  
ElasticInferenceAccelerators: インスタンスに接続するElastic Inferenceアクセラレーターの仕様を指定します。  
EnclaveOptions: Nitro Enclavesオプションを指定します。  

HibernationOptions: インスタンスのハイバーネーションオプションを指定します。  
HostId: 専用ホストのIDを指定します。  
HostResourceGroupArn: ホストリソースグループのARNを指定します。  

IamInstanceProfile: IAMインスタンスプロファイルを指定します。  
ImageId: インスタンスに使用するAMIのIDを指定します。  
InstanceInitiatedShutdownBehavior: インスタンスがシャットダウンされたときの動作を指定します。  
InstanceType: インスタンスのタイプを指定します。  
Ipv6AddressCount: インスタンスに割り当てるIPv6アドレスの数を指定します。  
Ipv6Addresses: インスタンスに割り当てるIPv6アドレスを指定します。  

KernelId: インスタンスに使用するカーネルIDを指定します。  
KeyName: インスタンスに使用するキーペアの名前を指定します。  

LaunchTemplate: ラウンチテンプレート仕様を指定します。  
LicenseSpecifications: インスタンスに適用するライセンス仕様を指定します。  

Monitoring: インスタンスのモニタリングを有効にするかどうかを指定します。  

NetworkInterfaces: インスタンスに接続するネットワークインターフェイスを指定します。  

PlacementGroupName: プレイスメントグループの名前を指定します。  
PrivateDnsNameOptions: プライベートDNS名オプションを指定します。  
PrivateIpAddress: インスタンスのプライベートIPアドレスを指定します。  
PropagateTagsToVolumeOnCreation: ボリューム作成時にタグを伝播するかどうかを指定します。  

RamdiskId: インスタンスに使用するRAMディスクIDを指定します。  

SecurityGroupIds: インスタンスに関連付けるセキュリティグループのIDを指定します。  
SecurityGroups: インスタンスに関連付けるセキュリティグループの名前を指定します。  
SourceDestCheck: ソース/宛先チェックを有効にするかどうかを指定します。  
SsmAssociations: SSM関連付けを指定します。  
SubnetId: インスタンスが所属するサブネットのIDを指定します。  

Tags: インスタンスに付与するタグを指定します。  
Tenancy: インスタンスのテナント属性を指定します。  

UserData: インスタンス起動時に実行するユーザーデータを指定します。  

Volumes: インスタンスに接続するボリュームを指定します。  