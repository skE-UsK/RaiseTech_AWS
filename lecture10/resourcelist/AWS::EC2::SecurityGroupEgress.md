# [AWS::EC2::SecurityGroupEgress](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-security-group-egress.html)

## 概要
VPC用のセキュリティグループに指定されたイグレスルールを追加するために使用されるAWS CloudFormationリソースです。アウトバウンドルールは、インスタンスが指定された宛先IPv4またはIPv6 CIDRアドレス範囲、または同じVPCの指定された宛先セキュリティグループにトラフィックを送信することを許可します。各ルールにはプロトコル（例えばTCP）が指定されます。

## プロパティの一覧
CidrIp: IPv4アドレス範囲（CIDR形式）です。宛先セキュリティグループ（DestinationPrefixListIdまたはDestinationSecurityGroupId）またはCIDR範囲（CidrIpまたはCidrIpv6）のいずれかを指定する必要があります。  
CidrIpv6: IPv6アドレス範囲（CIDR形式）です。宛先セキュリティグループ（DestinationPrefixListIdまたはDestinationSecurityGroupId）またはCIDR範囲（CidrIpまたはCidrIpv6）のいずれかを指定する必要があります。  

Description: ルールの説明です。  
DestinationPrefixListId: 宛先プレフィックスリストのIDです。  
DestinationSecurityGroupId: 宛先セキュリティグループのIDです。  

FromPort: トラフィックを許可するTCPおよびUDPプロトコルの開始ポート番号、またはICMPプロトコルのICMPタイプ番号です。

GroupId: セキュリティグループのIDです。

IpProtocol: トラフィックを許可するプロトコルです。  
ToPort: トラフィックを許可するTCPおよびUDPプロトコルの終了ポート番号、またはICMPプロトコルのICMPコード番号です。  

