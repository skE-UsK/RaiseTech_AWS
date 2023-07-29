# [AWS::ElasticLoadBalancingV2::TargetGroup](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-targetgroup.html)

## 概要
Application Load Balancer、Network Load Balancer、またはGateway Load Balancerのターゲットグループを指定するためのCloudFormationリソースタイプです。

## プロパティの一覧
HealthCheckEnabled: ヘルスチェックが有効かどうかを示します。  
HealthCheckIntervalSeconds: 個々のターゲットのヘルスチェックの間隔（秒単位）を指定します。  
HealthCheckPath: [HTTP/HTTPSヘルスチェック] ターゲットへのヘルスチェックの宛先を指定します。  
HealthCheckPort: ロードバランサーがターゲットに対してヘルスチェックを実行する際に使用するポートを指定します。  
HealthCheckProtocol: ヘルスチェックに使用するプロトコルを指定します。  
HealthCheckTimeoutSeconds: ヘルスチェックがタイムアウトするまでの時間（秒単位）を指定します。  
HealthyThresholdCount: ヘルスチェックが成功したと見なされるまでに必要な成功回数を指定します。  

IpAddressType: IPアドレスの種類（IPv4またはIPv6）を指定します。  

Matcher: HTTPコードまたはgRPCコードを指定して、ヘルスチェックが成功したかどうかを判断します。  

Name: ターゲットグループの名前を指定します。  

Port: ターゲットグループがトラフィックを受信するポート番号を指定します。  
Protocol: ターゲットグループがトラフィックを受信するプロトコルを指定します。  
ProtocolVersion: プロトコルバージョン（HTTP1またはHTTP2）を指定します。  

Tags: ターゲットグループに割り当てるタグのリストを指定します。  
TargetGroupAttributes: ターゲットグループ属性のリストを指定します。  
Targets: ターゲット記述子のリストを指定します。これらの記述子は、ターゲットグループに登録されるターゲットを記述します。  
TargetType: ターゲットタイプ（instance、ip、またはlambda）を指定します。  

UnhealthyThresholdCount: ヘルスチェックが失敗したと見なされるまでに必要な失敗回数を指定します。  

VpcId: ターゲットグループが作成されるVPCのIDを指定します。