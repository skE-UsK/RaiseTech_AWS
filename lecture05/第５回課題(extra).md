# `第５回課題（extra）`
## 課題
SDKを触ってみる。
<br/>
<br/>
<br/>


## はじめに
AWS Lambdaに触れてみようかなと思っていたらちょうど[参考](https://www.aws-room.com/entry/eventbridge-ec2-start)にできそうなものを見つけたのでMicrosoft Bingを使いながら触ってみた。  
違う言語を使う時にはEC2に何かインストールしないといけないかもと思ったので、サンプルアプリと同じrubyでプログラミングした。  
<br/>
<br/>

## ロール
AWS LambdaにRDSのフル権限を付与している。  
もっと絞っていいとは思う。  
<br/>
<br/>

## やってみた
とりあえず、rubyにしてもらった。   
![extra-1](images/extra/1.png)  
返ってきた
![extra-2](images/extra/2.png)  
必要なさそうなところを削っていく。  
渡されるjsonもシンプルにする。  
![extra-3](images/extra/3.png)  
返ってきたので実行してみる。  
![extra-4](images/extra/4.png)  
エラーをそのままコピペして聞く。  
![extra-5](images/extra/5.png)  
返ってきた通りに直して実行  
![extra-6](images/extra/6.png)  
コピペ  
![extra-7](images/extra/7.png)  
直す  
![extra-8](images/extra/8.png)  
エラーがなくなった。
![extra-9](images/extra/9.png)  
こんな感じで聞いて行ってEC2を停止した時にRDSを停止するRambdaができた。  
! extra-[end](images/extra/end.png)  
<br/>
<br/>

## Gemfileの編集
とりあえずサンプルアプリのGemfileに追記した。(必要ないかも？)
<br/>
<br/>

## ルール
[参考](https://www.aws-room.com/entry/eventbridge-ec2-start)の通りにやる。  
EC2が停止した時がトリガーだから全く同じ  
ターゲットもAWS Lambdaなので同じ  

RDSはあくまでAWS Lambdaが操作することに留意  


イベントバスにつていは謎。  
有効化にしないとダメかと思ったけど、無効にしても停止した。  

コードは間違っていてもデプロイできる。  
ロールは最初に設定しておかないとAWS Lambdaのテスト中にエラーが出る。  
RDS(Lambdaが操作するもの)も動いていないとエラーが出る。  
<br/>
<br/>

## 感想まとめ
EC2を勝手に立ち上げてくれてもしょうがないので、RDSを停止してくれるようにした。  
最初は自分で作るんだと意気込んでいたが、数行のコードなら簡単に作ってくれた。  
バケット操作や、スケジュールのルール変更はまたそのうちやろうと思う。  
<br/>
<br/>

## 参考
EventBridge を使用して EC2 インスタンスの停止を検知し再起動させる：[https://www.aws-room.com/entry/eventbridge-ec2-start](https://www.aws-room.com/entry/eventbridge-ec2-start)

https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/testing-functions.html




<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>




# 追記
## sudo service unicorn start等のコマンドが使えない
/bin/bathをいじってしまったのかなと思う  

```sh
sudo yum install --reinstall bash
```

インストールしなおしたら直った  
書き込み可能な状態で開くのは危険かもしれない  
```sh
view /bin/bash
vim -R /bin/bash
```
読み取り専用で開くといい  
<br/>
<br/>


## サンプルアプリが正しく表示されない
サンプルアプリのデプロイ中にcss周りでエラーが出て正しく表示されないことがあるらしい  

具体的には「application.debug-」の文字列を含む.cssファイル が net::ERR_ABORTED 404 (Not Found になる現象  

エラーは開発ツールで確認できるらしい  

この場合、デバッグを生成しないようにする設定へ変更すると解決することが確認されている
  
デバッグモードを無効にするには  
1. config/environments/development.rb ファイルを開く
1. config.assets.debug の値を false に設定する
> config.assets.debug = false

この変更により、正しく表示できたという報告があった  



