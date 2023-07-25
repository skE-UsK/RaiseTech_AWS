# `第１０回課題（２）`
## 課題
- CloudFormation を利用して、現在までに作った環境をコード化しましょう。
  - コード化ができたら実行してみて、環境が自動で作られることを確認してください。
- 結果を Discord で報告してください。
</br>
</br>

## はじめに
テンプレートを分けたくなったので分けた。  
テンプレートを分けて更新をすれば、既存のスタックの上にどんどん追加されていくのかと思ったら、そうではなかった。  

作れたスタックが削除されることにずっと悩んでいた。  

スタックの作成＞新しいリソースを使用（標準）とどんどん作成していけばいいだけだった。  

```yml
Outputs:
  一意の論理Id1:
    Value: !Ref アウトプットしたいリソースの論理ID
    Export:
      Name: ExportName
```
Outputs:セクションで、上記のように指定してアウトプットしたリソースを以下の形で使用することができる

```yml
Fn::ImportValue: ExportName
```
ExportNameは一意でないとならない

```yml
!Sub ${AWS::StackName}Id-VPC
```
スタック作成時にすでに存在する名前は使えないため、スタック作成時のNameを含めると便利。  


##　EC2の作成
【AWS】CloudFormationで、定番のネットワーク構成を作成してみた：[https://zenn.dev/anaka/articles/627d0a112d57ed](https://zenn.dev/anaka/articles/627d0a112d57ed)  
ここを参考に作っていく。  

```yml

  EC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      SubnetId: 
        Fn::ImportValue: !Sub ${ProjectName}Id-Subnet-Pub-AZa
      ImageId: !Ref OS
      KeyName: !Ref KeypairName
      SecurityGroupIds: 
        - !Ref InALB
        - !Ref In22SSH
        - !Ref OutAll
      Tags: 
        - Key: Name
          Value: !Sub "${ProjectName}-EC2"

```
AWS::EC2::Instanceプロパティを[一覧で見る](resourcelist/AWS::EC2::Instance.md)  

## Keypair
```yml

  NewKeyPair:
    Type: AWS::EC2::KeyPair
    Properties:
      KeyName: !Sub ${KeypairName}

```
AWS::EC2::KeyPairプロパティを[一覧で見る](resourcelist/AWS::EC2::KeyPair.md)  

キーペアを作成した。  
クラウドフォーメーションで作成すると、キーペアはダウンロードできない。  
キーペアは再発行ができないのでどうするのかわからない。  
今はなくても困らないので、作成する必要もなかったが、とりあえず作成した。  



## SecurityGroup
```yml

InALB:
  Type: AWS::EC2::SecurityGroup
  Properties:
    GroupName: 'InALB'
    GroupDescription: InALB
    VpcId:
      Fn::ImportValue: !Sub ${ProjectName}Id-VPC
    SecurityGroupIngress:
      - IpProtocol: tcp
        FromPort: 80
        ToPort: 80
        SourceSecurityGroupId: 
          Fn::ImportValue: !Sub ${ProjectName}Id-SG-In80HTTP
    Tags:
      - Key: Name
        Value: !Sub "[${ProjectName}]InALB@EC2"

```


yml分割したから参照先が複雑になったものの、基本は[lecture10-1](./lecture10-1.md)でやったことと同じ。  

ALBとSSHからのインバウンドと、すべてのプロトコル、すべてのポートからのアウトバウンドを許可した。  
デフォルトで許可されているのでわざわざ許可する必要はない。  

InALBのコードはセキュリティグループがソースになっているので、新しい。  
```yml
SourceSecurityGroupId: 
  Fn::ImportValue: !Sub ${ProjectName}Id-SG-In80HTTP
```


### ImageId
【CloudFormation / Terraform】EC2の最新版のAMI IDを自動的に取得、構築する (Windows / Linux)：[https://blog.serverworks.co.jp/automate-latest-ami-ec2#Amazon-Linux-2%E3%81%AE%E5%A0%B4%E5%90%88-1](https://blog.serverworks.co.jp/automate-latest-ami-ec2#Amazon-Linux-2%E3%81%AE%E5%A0%B4%E5%90%88-1)  
ここを参考にした。  

AMI IDは頻繁に更新が行われているらしく、ハードコードにしてしまうと数ヶ月後には使えなくなってしまうらしい。  
実際、新規で作成してみたら

lecture04  
AMI ID  
ami-0b51fe1c0254d8fc9  
AMI 名  
amzn2-ami-kernel-5.10-hvm-2.0.20230612.0-x86_64-gp2  
AMI の場所  
amazon/amzn2-ami-kernel-5.10-hvm-2.0.20230612.0-x86_64-gp2  

lecture10(現在)  
AMI ID  
ami-05ffd9ad4ddd0d6e2  
AMI 名  
amzn2-ami-kernel-5.10-hvm-2.0.20230628.0-x86_64-gp2  
AMI の場所  
amazon/amzn2-ami-kernel-5.10-hvm-2.0.20230628.0-x86_64-gp2  

確かに変わっていた。

パラメータセクションに以下を書くとEC2の最新版のAMI IDを自動的に取得してくれるらしいので書いた。

```yml
Parameters:
  OS:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: "/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2"
```
違うのだった。  

AMI ID
ami-0ebe0a87a50664c5a
AMI 名
amzn2-ami-hvm-2.0.20230628.0-x86_64-gp2
AMI の場所
amazon/amzn2-ami-hvm-2.0.20230628.0-x86_64-gp2

[lecture04](../lecture04/lecture04.md)でAmazon Linux 2023 AMIを選択して詰まったので、できることなら差異の少なそうなAMI ID :ami-05ffd9ad4ddd0d6e2 にしたいが、調べても出てこなかった。  

AMI の場所でできるかと思ってやってみたけど無理だった。  

できた。使えるパスとAMI の場所と名前を見比べて、それっぽくくっつけたらなんかできた。  
```yml
Parameters:
  OS:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: "/aws/service/ami-amazon-linux-latest/amzn2-ami-kernel-5.10-hvm-x86_64-gp2"

```



### 使用したリソース  
[AWS::EC2::SecurityGroup](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-security-group.html)

[AWS::EC2::Instance](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html)

[AWS::EC2::KeyPair](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-keypair.html)

</br>
</br>
</br>
</br>
</br>


<div style="text-align: center;">

[前へ](./lecture10-1.md)　／　[次へ](./lecture10-3.md)

</br>
</br>
</br>
</br>
</br>

