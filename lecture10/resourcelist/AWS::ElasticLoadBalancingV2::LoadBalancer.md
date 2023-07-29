# [AWS::ElasticLoadBalancingV2::LoadBalancer](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-loadbalancer.html)

## 概要
Application Load Balancer、Network Load Balancer、またはGateway Load Balancerを指定するためのCloudFormationリソースタイプです。

## プロパティの一覧
IpAddressType: IPアドレスの種類（IPv4またはIPv6）を指定します。  

LoadBalancerAttributes: ロードバランサー属性のリストを指定します。  

Name: ロードバランサーの名前を指定します。  

Scheme: ロードバランサーのスキーム（internet-facingまたはinternal）を指定します。  
SecurityGroups: ロードバランサーに関連付けるセキュリティグループのIDのリストを指定します。  
SubnetMappings: サブネットマッピングのリストを指定します。これらのマッピングは、ロードバランサーが配置されるサブネットとElastic IPアドレスを記述します。  
Subnets: ロードバランサーが配置されるサブネットのIDのリストを指定します。  

Tags: ロードバランサーに割り当てるタグのリストを指定します。  
Type: ロードバランサーのタイプ（application、network、またはgateway）を指定します。  
