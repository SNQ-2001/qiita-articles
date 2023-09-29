---
title: 【Swift】文字列内の"(ダブルクォーテーション)をエスケープするのがめんどくさい
tags:
  - iOS
  - Swift
private: false
updated_at: '2023-09-11T21:54:12+09:00'
id: 9becd9a3d4fac46a541f
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
SwiftでJSONを文字列で定義しようとするとこんな感じになります

![スクリーンショット 2023-09-11 21.51.53.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/4e2d7784-c20f-90b7-389d-1020ed8e3a55.png)

これを解決するためにバックスラッシュでエスケープします

![スクリーンショット 2023-09-11 21.51.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/70bd7e00-f3ff-119d-451e-63cf170edb5d.png)

ただ、これがめんどう！！

これをしなくていい方法があります

# やりかた
`#`で囲むだけでOK!
```swift
let text = #"{"name": "Taishin", "age": 22}"#
```

![スクリーンショット 2023-09-11 21.52.14.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/7217132d-db32-a362-0039-7cdbc51a72ba.png)

# おわり
めっちゃ簡単ですね
