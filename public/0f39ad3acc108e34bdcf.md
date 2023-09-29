---
title: 【VSCode】ファイルツリー構造のインデントが浅くて見づらい
tags:
  - VSCode
private: false
updated_at: '2023-09-08T21:34:29+09:00'
id: 0f39ad3acc108e34bdcf
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
最近、VSCodeを使うことが多くなりました。
Xcodeに慣れている自分にとって、VSCodeのファイルツリーはインデントが浅くて見づらいです。
変更することができるっぽいのでやり方を記録しておきます。

# こうなる
|before|after|
|-|-|
|![スクリーンショット 2023-09-08 21.32.50.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/84677ff8-7e5e-459e-a274-79a526cc8284.png)|![スクリーンショット 2023-09-08 21.32.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/002b7384-6f8a-fff8-8635-f011f8a0e218.png)|

# やりかた
① 「Code」を選択します
② 「基本設定」を選択します
③ 「設定」を選択します
![スクリーンショット 2023-09-08 21.26.43.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/3c7f9c9a-9204-5c38-f1fc-9f3d8193fa9d.png)

④ `tree indent`を検索します
![スクリーンショット 2023-09-08 21.29.14.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/172672b6-f82d-d455-3600-442741067e85.png)

⑤ 「Workbench > Tree Indent」の数値を変更します
![スクリーンショット 2023-09-08 21.30.24.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/fbb5d793-ecbd-e028-1586-5d44912de070.png)

# おわり
めっちゃ見やすくなりました！
