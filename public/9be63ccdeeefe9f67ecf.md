---
title: 【Xcode】MacOSアプリをリリースしようとしたらエラーが出た
tags:
  - Xcode
  - macOS
  - リリース
  - Swift
private: false
updated_at: '2023-01-22T18:35:42+09:00'
id: 9be63ccdeeefe9f67ecf
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
久しぶりにMacOSアプリをリリースしようとしたらエラーが出たので記録しておきます。

# エラー
![スクリーンショット 2023-01-22 16.46.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/4039c88e-c2c9-bd5c-9ec3-f0b2cd02ca26.png)
```
The product archive is invalid. The Info.plist must contain a LSApplicationCategoryType key, whose value is the UTI for a valid category. For more details, see "Submitting your Mac apps to the App Store". (ID: 54c62bd4-c581-4e3e-bdb3-f2c526f64d9c)
```

# 解決方法
① プロジェクトを選択します
② ターゲットを選択します
③ 「General」を選択します
④ 「App Category」をタップします
![スクリーンショット 2023-01-22 17.00.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/f5965468-2c45-33f0-5907-e60dc1d40a69.png)

⑤ カテゴリーの中から自分のアプリに合うものを選択します
![スクリーンショット 2023-01-22 18.28.47.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/3f5f7229-f685-97f3-f8ae-e8a6b12dd506.png)

# おわり
もう1度「Archive」を行うと通るようになります。
