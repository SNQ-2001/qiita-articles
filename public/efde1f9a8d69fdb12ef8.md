---
title: 【Swift Playgrounds】iPadでリリースしたアプリをMacで管理したい
tags:
  - Swift
  - SwiftPlaygrounds
  - SwiftUI
private: false
updated_at: '2022-06-22T16:47:46+09:00'
id: efde1f9a8d69fdb12ef8
organization_url_name: null
slide: false
ignorePublish: false
---
# 状況
iPad版SwiftPlaygroundsでアプリをリリースしたが、慣れているMac(Xcode)でメンテをしたい。

# 条件
- Xcodeで編集したい
- SwiftPlaygroundsにも残しておきたい
- Xcodeでの編集をSwiftPlaygroundsに反映させたい

# 方法
## iPadのiCloud Driveを有効にする
![IMG_2499.PNG](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/931da063-c9b7-c9e5-bc34-2775e7718db7.png)

## MacのiCloud Driveを有効にする
![スクリーンショット 2022-06-22 16.35.45.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/29c9e79a-ddaf-a8ce-1342-86e6e0648253.png)

## Finderからswiftpmを開く
`アプリ名.swiftpm`をダブルタップします
![スクリーンショット 2022-06-22 16.33.29.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/f0e9cef7-2f89-5963-a3db-bf50a52dead7.png)

「Trust and Open」を選択
![スクリーンショット 2022-06-22 16.38.04.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/18a45632-737e-2408-93a0-69ae8652770f.png)

このような感じになっています。

![スクリーンショット 2022-06-22 16.41.17.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/a4d366c7-dc84-9753-3528-c6c49a4e717b.png)

# おわり
iPad、Mac共にiCloud Driveが有効であれば変更がすぐに反映され結構便利です。

1つ驚いたのがプレビュー用のstructがなくてもプレビューが表示されています笑
