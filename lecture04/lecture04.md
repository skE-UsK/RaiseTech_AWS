# `第４回課題`
## 課題
- AWS 上に新しく VPC を作ってください。
- EC2 と RDS を構築してください。
- EC2 から RDS へ接続し、正常であることを確認して報告してください。
<br/>
<br/>
<br/>

## はじめに  
スライド資料の手順で作成していたが、自分が何をしているのかわからなくなってしまった。  
理由は、勝手に作られてしまうものが多いためで、全体像がどうなっているのか把握できなくなってしまったためだと思われる。  
なので、一つずつ作成・確認しながらスライド資料にある図と同じものを作成する。

具体的には、同一のVPC内にパブリックサブネットとプライベートサブネットを作成し、それぞれにセキュリティグループを適用しつつ、パブリックサブネットにはEC2をプライベートサブネットにはRDSを配置する。
<br/>
<br/>
<br/>

## AWS 上に新しく VPC を作ってください。
## VPCの作成  
![１](images/makeVPC/1.png)  
IPv4 CIDR を10.0.0.0/16 で作成する。  
分かりづらいので２進数にする。  
IPアドレス：00001010.00000000.00000000.00000000  
サブネットマスク：11111111.11111111.00000000.00000000  
ネットワーク部：ホスト部  
00001010.00000000：00000000.00000000  
![map](images/makeVPC/map.png)  
VPCが作成できた。

### [VPC（仮想プライベートクラウド）](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/configure-your-vpc.html)
VPC ( Virtual Private Cloud ) は、AWS アカウント専用の仮想ネットワークです。VPC は、AWS クラウドの他の仮想ネットワークから論理的に切り離されています。VPC 内には、Amazon EC2 インスタンスなどの AWS リソースを起動できます。
<br/>
<br/>
<br/>

## サブネットの作成  
![１](images/makeSubnet/1.png)  
作成したVPCを選択し、その中にサブネットを作成する。  
作成するサブネットは同一のAZ(ap-northeast-1a)内に２つ作り、それぞれをパブリックサブネット、プライベートサブネットにする。  
パブリックサブネット  
10.0.10.0/24  
IPアドレス：00001010.00000000.00001010.00000000  
サブネットマスク：11111111.11111111.11111111.00000000  
ネットワーク部：ホスト部  
00001010.00000000.00001010：00000000  

プライベートサブネット  
10.0.20.0/24  
IPアドレス：00001010.00000000.00010100.00000000  
サブネットマスク：11111111.11111111.11111111.00000000  
ネットワーク部：ホスト部  
00001010.00000000.00010100：00000000  
![map](images/makSubnet/map.png)  
サブネットが２つできた。

### [サブネット](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/configure-subnets.html)
サブネットは、VPC の IP アドレスの範囲です。特定のサブネットには、EC2 インスタンスなどの AWS リソースを作成できます。
<br/>
<br/>
<br/>

## インターネットネットゲートウェイの作成  
![１](images/makeIGW/1.png)  
IGWを使用するVPCが選べないため不安になったが、名前をつけて作成すると  
![２](images/makeIGW/2.png)  
ポップが出てきたのでアタッチする。  
ポップ以外の方法は、一覧からアタッチ・デタッチが選べる。  
![３](images/makeIGW/3.png)  
VPCを選択してアタッチする。  
![map](images/makeIGW/map.png)  
ネットワーク接続が追加されたが、アタッチしただけではルートテーブルからは繋がらない。

### [インターネットゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)
VPC とインターネットとの間の通信を可能にする VPC コンポーネントであり、冗長性と高い可用性を備えており、水平スケーリングが可能です。IPv4 トラフィックおよび IPv6 トラフィックをサポートしています。ネットワークトラフィックに可用性のリスクや帯域幅の制約が発生することはありません。
<br/>
<br/>
<br/>

## ルートテーブルの編集  
![１](images/rootSettig/1.png)  
0.0.0.0/0はすべてのアドレスの意味。  
![map1](images/rootSetting/map1.png)  
プライベートサブネットからもネットワーク接続へ伸びているのがおかしいと思う。  
![２](images/rootSettig/2.png)  
パブリックサブネットのパブリック IPv4 アドレスの自動割り当てを有効化にした。  
これをしないとインターネットに接続できないらしいので、プライベートサブネットではインターネットに接続できない？  

どうやら今回のように複数のサブネットが存在して、それぞれ通信ルートが異なる場合は、サブネットを作った時に勝手にできるルートテーブルは使用しないで、新しくルートテーブルを作成して割り当てた方が良いらしい。  
![３](images/rootSettig/3.png)  
新規に作って、ルートを編集する。（先ほどの編集は削除する。自動割り当てはそのまま）  
![map2](images/rootSetting/map2.png)  
新しくルートテーブルが作成された。  

![４](images/rootSettig/4.png)  
アクションからサブネットの関連付けを選択して  
![５](images/rootSettig/5.png)  
IGWに繋げる（パブリックサブネットにしたい）サブネットを選択する。  
![map3](images/rootSettig/3.png)  
プライベートサブネットからネットワーク接続への波線が消えた。

### [ルートテーブル](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Route_Tables.html)
ルートテーブルには、サブネットまたはゲートウェイからのネットワークトラフィックの経路を判断する、ルートと呼ばれる一連のルールが含まれます。
<br/>
<br/>
<br/>

## EC2 と RDS を構築してください。
## EC2 の構築
![１](images/makeEC2/1.png)  
インスタンスを起動  
![２](images/makeEC2/2.png)  
EC2の名前  
![３](images/makeEC2/3.png)  
OSを決める。Linuxを選択し、無料利用枠の対象になっているか確認  
![４](images/makeEC2/4.png)  
インスタンスタイプも無料利用枠の対象になっているか確認   
![５](images/makeEC2/5.png)  
キーペア名を決めて新しいキーペアの作成  
![６](images/makeEC2/6.png)  
ネットワーク設定を編集する。
- 作成したvpcを選択
- 作成したパブリックサブネットを選択
- セキュリティグループ名を変更
  
![７](images/makeEC2/7.png)  
インスタンスのストレージは課題３で変更したので保留。  
![８](images/makeEC2/8.png)  
高度な詳細はとりあえず保留。  
![９](images/makeEC2/9.png)  
インスタンスを起動をクリックするとインスタンスが起動するので、停止する。（ここまでをまとめるため）  
![end](images/makeEC2/end.png)  
ここでRDS データベースに接続するを選択すれば終わるのかもしれない。  
![pingコマンド](images/makeEC2/ping.png)  
インターネットにつながっているか確認した。  
![pingコマンド](images/makeEC2/error.png)  
ルートテーブルを編集してパブリックサブマスクをIGWに繋げないでインスタンスを起動してみたらそもそも使えなくなった。  

<br/>
<br/>
<br/>

## RDS の構築
問題が発生した。  
データベースを作成しようとしたらエラーが出てきて、作成ができなかった。  
![エラー](images/makeDB/error.png)  
どうやらAZが少なくとも２つないとDBの作成はできないらしい。

そのため、サブネットを修正する。

変更前  
ap-northeast-1a
10.0.10.0/24 パブリックサブネット 
10.0.20.0/24 プライベートサブネット  

変更後  
ap-northeast-1a  
10.0.10.0/24 パブリックサブネット  
ap-northeast-1d  
10.0.20.0/24 プライベートサブネット  
![map](images/makeEC2/map.png)  


![１](images/makeDB/1.png)  
標準作成を選択  
![２](images/makeDB/2.png)  
MySQLを選択。課題３で使った8.0.33はなかった。  
![３](images/makeDB/3.png)  
テンプレートで無料利用枠を選択すると、可用性と耐久性は選べない。
![４](images/makeDB/4.png)  
インスタンス識別子とパスワードを決める。マスターユーザー名はそのまま  
![５](images/makeDB/5.png)  
インスタンス設定は選べないのでそのまま  
ストレージの自動スケーリングを有効にするのチェックを外す  
![６](images/makeDB/6.png)  
EC2 コンピューティングリソースに接続を選択すれば次の課題も終わると思われるが、今回はEC2 コンピューティングリソースに接続しないを選択する。
VPCを選択する  
![７](images/makeDB/7.png)  
セキュリティグループを新規で作成し、名前を決める  
AZを選択する  
![８](images/makeDB/8.png)  
何もいじるところはない  
![９](images/makeDB/9.png)  
月額　21.74 USD = 3,074.01 円　かかるらしい。
<br/>
<br/>

### 余談
変更前  
ap-northeast-1a  
10.0.10.0/24 パブリックサブネット  
10.0.20.0/24 プライベートサブネット  

変更後  
ap-northeast-1a  
10.0.10.0/24 パブリックサブネット  
10.0.20.0/24 プライベートサブネット  
ap-northeast-1d  
10.0.30.0/24 プライベートサブネット  

当初このように、単純にAZを追加する形で修正をし、データベースを作成したが、ap-northeast-1aにあるプライベートサブネットが不要な気がしたので、データベースとサブネットを削除して現在の形に作り直した。  

その際にかなり詰まったので、簡単にまとめる  
![エラー２](images/makeDB/error2.png)  
ap-northeast-1dにサブネットがないから新しく作るか、ap-northeast-1aから選択してくれ  
サブネットは作成してあるので、ap-northeast-1aを選択すると  
![エラー２](images/makeDB/error.png)  
少なくとも２つのAZをカバーするようにサブネットを追加してくれ  
最初のエラーに戻ってしまった。

わからないのでディスコードで質問すると、DBサブネットグループが怪しいとのことだったので確認したら解決した。

このRDSで作成されるのは３つ
- データベースインスタンス
- DBサブネットグループ
- VPCセキュリティグループ

データベースを削除してもDBサブネットグループとVPCセキュリティグループは残り続け、新たにデータベースを作成しようとすると、どうやらその残った設定を適用しようとする仕様らしい。  

DBサブネットグループを削除したら新しく作成できた。  

この過程で調べるうちにシングルAZとマルチAZがあるらしいことがわかった。  
シングルAZでは１つのAZ内にEC2とRDSがまとまっている構成ができるらしいが、再現できなかった。  
<br/>
<br/>
<br/>

## EC2 から RDS へ接続し、正常であることを確認して報告してください。

全然できなかったので、EC2インスタンスとDBインスタンスを削除して、作り直した。
その際に
![３](images/makeEC2/3.png)  
![６](images/makeDB/6.png)  
EC2インスタンス起動時にはAmazon Linux 2023 AMIではなく、Amazon Linux 2 AMI (HVM) - Kernel 5.10, SSD Volume Typeを選択し、RDS作成時のEC2 コンピューティングリソースに接続を選択してみたらそのほか何も設定することなく接続することができた。  
![map](images/ec2-db/map.png)  
勝手にサブネットを３つ作られた。  
![end](images/ec2-db/end.png)  
課題は達成したが、理解はできていないため、削除して作り直す。  

どうせならとVPCも消して、1からやってみた。  
起動できた。  

### 接続方法
EC2インスタンス起動時にはAmazon Linux 2023 AMIではなく、Amazon Linux 2 AMI (HVM) - Kernel 5.10, SSD Volume Typeを選択して、今回はEC2 コンピューティングリソースに接続しないを選択する。
![1](images/ec2-db/1.png)  
RDSの作成が完了したら、EC2 接続のセットアッフをクリック
![２](images/ec2-db/2.png)  
接続するインスタンスを選択する。インスタンスは起動していないと表示されない。  
![３](images/ec2-db/3.png)  
確認とセットアップをクリック
![４](images/ec2-db/4.png)  
するとセキュリティグループが２つ（ec2-rds-1 と rds-ec2-1）作成される。
![５](images/ec2-db/5.png)  
rds-ec2-1を適用する。

実行するコマンド
```sh
sudo yum install mysql
```
実行するとインストールが始まる。Amazon Linux 2023 ではこのコマンドが使えなかった。  

実行するコマンド
```sh
mysql -u admin -p -h データベースのエンドポイント
```
実行するとパスワードの入力を求められる。RDS作成時に決めたパスワードを入力するとRDSへ接続ができる。

このコマンド実行時にセキュリティグループの設定が正しくないとパスワードを入力してEnterを押しても改行がされるだけになる。（Control + C で抜けられる）
<br/>
<br/>
<br/>

###　セキュリティグループについて
インバウンド  
ec2-rds-1　タイプ：MYSQL/Aurora プロトコル：TCP ポート範囲：3306 ソース：rds-ec2-1  
このセキュリティ グループがアタッチされているインスタンスから db-lecture04 への接続を許可するルール  
このセキュリティグループは接続するEC2に勝手に追加される。  

アウトバウンド  
rds-ec2-1 タイプ：MYSQL/Aurora プロトコル：TCP ポート範囲：3306 ソース：ec2-rds-1  
ec2-rds-1 がアタッチされた EC2 インスタンスからの接続を許可するルール  
このセキュリティグループはデータベースに自分で追加する。  
<br/>
<br/>
<br/>


## 参考
AWSのネットワーク構築手順：[https://smallit.co.jp/blog/a1019/](https://smallit.co.jp/blog/a1019/)

【AWS】パブリックサブネットとプライベートサブネットを持つVPCの構築：[https://www.hanatare-papa.jp/entry/technology-aws-vpc-1-446](https://www.hanatare-papa.jp/entry/technology-aws-vpc-1-446)


Multi-AZとは?マルチAZ構成のメリット・デメリットについても解説：[https://www.rworks.jp/cloud/aws/aws-column/aws-entry/22067/](https://www.rworks.jp/cloud/aws/aws-column/aws-entry/22067/)

AWSで障害対策に必須のマルチAZとは？：[https://www.stylez.co.jp/columns/what_is_multi_az/](https://www.stylez.co.jp/columns/what_is_multi_az/)


【初心者向け】EC2からRDSへ接続してみた[https://blog.serverworks.co.jp/ec2-to-private-rds](https://blog.serverworks.co.jp/ec2-to-private-rds)




