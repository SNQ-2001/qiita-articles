---
title: 【Xcode】NSLogを非表示にする
tags:
  - Xcode
  - iOS
  - NSLog
  - Swift
private: false
updated_at: '2022-07-12T15:55:06+09:00'
id: 2ea9c9a4c3f08eacade2
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
動作には問題のない警告文が大量に出てきて鬱陶しかったのでログを非表示にしました
あんまり良くないとは思うのでやらない方がいいと思います。

需要はないと思いますけど一応やり方を紹介しておきます。

# NSLogとは
`print`との違いは日時を表示してくれる点です。
![スクリーンショット 2022-07-12 15.36.25.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/948736cc-31c6-50fa-758c-acd2c1b408f4.png)

# やり方
画像の赤枠内をクリックします。
![スクリーンショット 2022-07-12 15.40.35.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1e5be67c-efb9-51de-d0e0-4390b7470bd0.png)
クリックするとポップアップが表示されるので「Edit Scheme...」を選択します。
![スクリーンショット 2022-07-12 15.41.35.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/5cfd57da-0595-9bd7-6cf0-db2f027f6ee3.png)
① 「Run」を選択します。
② 「Arguments」を選択します。
![スクリーンショット 2022-07-12 15.43.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/8b8d2f5e-9fb8-2675-80a9-2dc9df1c97ec.png)
① 「+」を押します。
② 「Name」に`OS_ACTIVITY_MODE`,「Value」に`disable`を入力します。
③ 「Close」を選択します。
|Name|Value|
|-|-|
|OS_ACTIVITY_MODE|disable|

![スクリーンショット 2022-07-12 15.49.03.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/cf581ab8-7efc-c77d-6944-d6cb7c1bbc1d.png)

NSLogのみ表示されなくなりました。
![スクリーンショット 2022-07-12 15.53.58.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/625b72ff-f5b2-61a8-bbfb-c2c767113e63.png)

# おわり
NSLogに関してはこのような情報もありました。
[[Swift] NSLogを安易に使ってしまうとセキュリティ的にマズい](https://qiita.com/y-some/items/448621066ccaa70cb0e7)

ログを覗かれる可能性があるのは怖いですね
