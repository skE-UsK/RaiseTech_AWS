# addについて
```sh
git add -u 
```
(git add --update)
バージョン管理されていて、変更があったすべてのファイルがaddされる
変更されたファイル、削除されたファイルがaddされる
バージョン管理されていないファイルはaddされない
新しく作られたファイルはaddされない

```sh
git add -A 
```
(git add --all)
変更があったすべてのファイルがaddされる
変更されたファイル、削除されたファイル、新しく作られたファイル、すべてがaddされる


```sh
git add .
```
カレントディレクトリ以下の、変更があったすべてのファイルがaddされる
カレントディレクトリ以下の、変更されたファイル、削除されたファイル、新しく作られたファイル、すべてがaddされる
git ver.1.xまでは、削除されたファイルはaddされなかった

[参考](https://note.nkmk.me/git-add-u-a-period/)



