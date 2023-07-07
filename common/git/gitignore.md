

# 特定のディレクトリをgitで管理しない手順

```sh
touch .gitignore
```
.gitignoreファイルを作成する  

```sh
vi .gitignore
```
.gitignoreを編集する。  
正直、open コマンドの方が楽  
管理しないディレクトリ名を入力する  
例
.DS_Store
vi コマンドは:wq で保存して終了  

```sh
git rm -r --cached . 
```
管理しているキャッシュを削除  
ローカルからは消えない。  
-r オプションを使うと下層にあるディレクトリも対象になる  

```sh
git add .
```
変更のあったものが対象  

```sh
git commit -m ".gitignore を追加" 
```
コミット  

```sh
git push origin branchName
```
プッシュ  
[参考](https://yana-g.hatenablog.com/entry/2020/10/26/134609)






