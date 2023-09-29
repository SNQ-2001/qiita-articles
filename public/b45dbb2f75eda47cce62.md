---
title: 【Xcode】「AST Deserialization Issue」を修正した
tags:
  - Xcode
  - iOS
  - Swift
  - 個人開発
private: false
updated_at: '2022-08-29T07:24:49+09:00'
id: b45dbb2f75eda47cce62
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
実機でビルドしようと思ったら突然大量のエラーが発生しました。


# エラー
![スクリーンショット 2022-08-25 23.34.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/fb02daeb-b2b4-53ff-52f5-78260ce2ffb1.png)

```
/Users/XXXXXXXXX/Library/Developer/Xcode/DerivedData/XXXXX-cjjyountbftezrcatmquboljpsyt/SourcePackages/checkouts/SDWebImage/SDWebImage/Core/SDWebImageCompat.h:67:10: File '/Users/XXXXXXXXX/Library/Developer/Xcode/DerivedData/ModuleCache.noindex/25U36CV5033SC/UIKit-2LM3EQU7VVY4O.pcm' is not a valid precompiled module file
```

# 原因
不明

誰かわかる方教えてください。

参考にした記事ではMacのアカウント名を変更した時になったらしいんですけど、自分は何も変更してないのに突然発生しました。

# 解決方法
メニューバーにある「Xcode」を押します。
![スクリーンショット 2022-08-25 23.37.21.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/d012f60c-be45-3df5-de6e-410d5ed14524.png)

「Preferences...」を選択します。
![スクリーンショット 2022-08-25 23.38.05.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0c75cf62-dd00-40b1-8ad5-841dd94f9a68.png)

① 「Locations」を選択します。
② 「Derived Data」を押します。
![スクリーンショット 2022-08-25 23.39.09.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/263409ec-753b-d5f1-100c-35082cd67694.png)

「Relative」を選択します。
![スクリーンショット 2022-08-25 23.40.41.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/30cc8058-214c-8e98-704c-285c80069a1e.png)

おわり

# 参考記事
https://teratail.com/questions/138830
