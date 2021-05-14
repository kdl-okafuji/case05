# 誤ってsecret key 等の情報をコミットしてしまった時の対策

## 0. リポジトリを作成しよう。
urlをはる
フォークする

## 1. 機密情報の書かれたファイルをコミットする
```
$ git switch -c feature/01

# 機密情報の書かれたファイルを作成
$ touch .env
$ echo "secret=123456789" > .env

$ touch sample.txt
$ echo "hello, world" > sample.txt
$ git add .env
$ git add sample.txt
$ git commit -m 'commit No.1'
$ git push origin feature/01
```

プルリクエスト作成までのスクショ
プルリクエスト時に注意する。
mainブランチにマージする

```
$ git switch main
$ git pull origin main
$ git branch -d feature/01
```

## 2. 現在のコミット状況の確認

TOP
ソース詳細 あることを確認
コミット詳細あることを確認
中身
github上で確認
コミット内に機密情報の変更履歴があることを確認。

## 3. git管理から.envファイルを削除してみましょう。
```
$ git switch -c feature/02
$ git rm .env
$ git add .env
$ git commit 'remove .env'
$ git push origin feature/02
```

プルリクエスト作成
mainブランチにマージする

## 4. 現在のmainブランチの状況を確認してみましょう。

TOP
ソース詳細 あることを確認
コミット詳細あることを確認
中身
- git管理されているソースコードの内容
- コミット履歴

**コミット履歴からは消えていないことがわかりますね！**

## 5. gitの変更履歴から.envファイルを削除してみましょう。
```
# treeからの削除
$ git filter-branch --index-filter "rm -f .env" HEAD
# 全リモートブランチに反映
$ git push origin --force --all

```

## 6. コミット履歴から削除できているか見てみましょう。


