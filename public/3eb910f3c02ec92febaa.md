---
title: 【Mac】ターミナルでスペースがはいったファイルを扱う
tags:
  - Mac
  - Terminal
  - パス
private: false
updated_at: '2023-01-19T19:50:10+09:00'
id: 3eb910f3c02ec92febaa
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
名前にスペースがはいってるフォルダを扱ってる時にパスがうまく指定できませんでした。
対策を知ったので記録しておきます。

以下のようなスペースのはいったフォルダを作成して例にしてみます。
![スクリーンショット 2023-01-19 19.45.25.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/70874dc5-a316-2101-6444-f52180c2277d.png)

# 対策
スペースの前に`\`を挿入します
### 良い例
```
/Users/miyamototaishin/Desktop/sample folder
```
### 悪い例
```
/Users/miyamototaishin/Desktop/sample\ folder
```

# おわり
意外と見落としがちで原因探しに時間がかかっちゃうことがあります。
時間がもったいないので覚えておきましょう。
