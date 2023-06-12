# 第２回 課題について
## 所見
&emsp;2023.05.26〜2023.05.30まで５日かかってようやくリポジトリの作成からマージまでの一連の流れを行う事ができた。

## 学んだこと
- GitとGitHub
- Markdownの書き方

### GitとGitHubの操作

#### １日目
&emsp;設定をした
```sh
> git config --global init.defaultBranch main
```
新規リポジトリのデフォルトブランチ名をmainに変更する設定。
```sh
> git config --global user.name "ユーザー名"
> git config --global user.email "メールアドレス"
```
ユーザー名とメールアドレスを設定する。
```sh
> git config -l
```
設定の一覧が見られる。

設定できていたら次のように確認できる。
```sh
> init.defaultbranch=main
> user.email="メールアドレス"
> user.name="ユーザー名"
```
#### ２日目
##### リポジトリを作った

&emsp;GitHubの右上にある*＋*から*New repository*を選択してリポジトリを作成した(RaiseTech)。

##### ホームディレクトリの名前を変更した

&emsp;課題とは関係ないが、ターミナルに表示されるホームディレクトリがフルネームで長く、入力がメンドイので変更した。

1. 別管理者アカウントを追加
2. 変更したいアカウントから別管理者アカウントへ移動
3. Finderのメニューバーから「移動」＞「フォルダへ移動』
4. 「/ユーザ」と入力して「return」キーを押す
5. 新しく名前を変更
6. パスワードの入力

&emsp;手順を知ってしまえば数分で終わる作業に結構時間がかかった。


#### ３日目

&emsp;２日目とは別のリポジトリ(Test)を作成してプッシュまでを行った。
&emsp;動画を見ながらやったのでわかった気になれた。

#### ４日目

&emsp;３日目にプッシュしたリポジトリ(Test)を確認したら中身にtest.txtがなく空だった。わかった気になっただけでできていなかった。
&emsp;ユーザー名とパスワードを入力する方法はサービスが終了しているらしく、トークンを作成しなければいけない事がわかった。
&emsp;エラーが出ていたのに英語だから気づかなかった。

#### ５日目
&emsp;どうにもならないのでディスコードで質問した。
&emsp;補足資料に全部書いてあった。

&emsp;原因は個人アクセストークン（PAT）に書き込み権限を与えていないからだった。
##### PAT取得手順
1. GitHub右上アイコンからsettingsを選択
2. 左のサイドバーからDeveloper settingを選択
3. personal access tokens　の　Fine-grained tokensを選択
4. Generate new token　を押すとパスワード入力
5. Token name　Expiration　Descriptionを決める
6. Repository accessをAll repositoriesに変更（ここがデフォルトだと読み込み専用）
7. PermissionsのRepository permissions
からcontents を探してSelect an access levelを Read and writeに変更（よくわからない）

&emsp;これも手順を知ってしまえば数分で終わる作業だった。


&emsp;pushする際パスワードを聞かれるらしいが、APT書き込み権限事件の試行錯誤の中で、sshを使用したGitHubへの接続ができるようになっていたため必要なかった。

##### GitHubの流れ
1. アクセストークンの作成
2. リポジトリの作成
3. クローンと移動
```sh
git clone URL
```
4. ブランチの作成と切替
```sh
git git switch -c test
```
5. ファイルの作成・変更
6. ファイルのステージング
```sh
git add -A
```
7. ファイルのコミット
```sh
git commit -m "コメント"
```
8. ステージング情報のプッシュ
```sh
git push origin branchName
```
9. プルリクエスト
10. マージ
11. ローカルリポジトリの更新


### Markdown
#### ３日目
&emsp;２日目に作ったREADME.mdの中身をいじってMarkdownを学んだ。
#### ５日目
&emsp;このlecture02.mdの作成

