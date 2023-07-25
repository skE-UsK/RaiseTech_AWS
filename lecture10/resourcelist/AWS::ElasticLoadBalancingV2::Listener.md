# [AWS::ElasticLoadBalancingV2::Listener](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-listener.html)

## 概要
Application Load Balancer、Network Load Balancer、またはGateway Load Balancerのリスナーを指定するためのCloudFormationリソースタイプです。リスナーは、ロードバランサーに着信するトラフィックを処理し、適切なターゲットグループに転送します。

## プロパティの一覧
AlpnPolicy: ALPNポリシーのリストを指定します。これらのポリシーは、TLSネゴシエーション中に使用されるアプリケーション層プロトコルを制御します。  

Certificates: 証明書のリストを指定します。これらの証明書は、HTTPSまたはTLSリスナーで使用されます。  

DefaultActions: デフォルトアクションのリストを指定します。これらのアクションは、リスナールールに一致しない要求に適用されます。  

LoadBalancerArn: リスナーが関連付けられるロードバランサーのAmazon Resource Name (ARN)を指定します。  

Port: リスナーがトラフィックを受信するポート番号を指定します。  
Protocol: リスナーがトラフィックを受信するプロトコルを指定します。  

SslPolicy: SSL/TLSポリシーを指定します。このポリシーは、HTTPSまたはTLSリスナーで使用されます。