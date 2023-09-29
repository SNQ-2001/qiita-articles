---
title: 【Swift】UIの階層を確認する
tags:
  - Xcode
  - iOS
  - UIKit
  - Swift
  - SwiftUI
private: false
updated_at: '2022-07-15T12:09:36+09:00'
id: e5dde7ab5ffe88fa4182
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
めっちゃ最近知った便利な機能「View UI Hierarchy」をちょっと調べてみました。

最近作った[こちら](https://github.com/SNQ-2001/FontAwesome-Swift)のサンプルアプリで試してみます。

# 表示方法
アプリをビルドします。
![スクリーンショット 2022-07-14 16.38.21.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/8f90c2d8-6d9c-13d3-5f28-a5e800b91c62.png)
① スプレーのようなアイコンを選択します。
② 縦３本線のアイコンを選択します。
![スクリーンショット 2022-07-14 16.39.50.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/26ae0722-b489-3bfe-8ed0-f5394cad5b2e.png)
「View UI Hierarchy」を選択します。
![スクリーンショット 2022-07-14 16.41.47.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/6c55387d-6ee4-6ee0-2991-e703d13bf5b1.png)

表示されました。
![スクリーンショット 2022-07-14 16.43.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/11fff337-3757-7594-0bc8-1ec2bd70599b.png)

# 立体にする
## 自動
立方体アイコンのボタンを押すと自動で立体になります。
![スクリーンショット 2022-07-14 16.50.04.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/6ac92c80-a06c-239d-d6e2-b34c10f9e5b5.png)

## 手動
左下のスライダーを右にスライドすると立体になります。
![スクリーンショット 2022-07-14 16.45.07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1ca3782c-0c00-894b-540a-448bf1d8374b.png)

# 階層ごとに表示
右下のスライダーを左にスライドすると上位の階層が非表示になります。
![スクリーンショット 2022-07-14 16.47.01.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/80bd9b8b-9055-25f4-b72a-6b21c80d7ef0.png)

# おわり
他にも機能がありますがよく理解してないので紹介するのはやめておきます笑
