---
title: 【SwiftUI】Menuのボタン順番について
tags:
  - iOS
  - Swift
  - menu
  - SwiftUI
private: false
updated_at: '2022-11-26T22:14:21+09:00'
id: f801e9abde1e459bc8bf
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
意識したことがないとあまり気づかないと思うのですが、
`Menu`内のボタンの表示される順番は、
`Menu`の`label`に近い方向から順番に表示されます。

|||
|-|-|
|![スクリーンショット 2022-11-26 22.09.16.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/70f5ed16-ec17-1345-23ad-42c65749724a.png)|![スクリーンショット 2022-11-26 22.09.24.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/93465353-7186-5760-56ef-c014a490a5d7.png)|

どこに配置されていても上から表示されてほしい場合があります。
そんな時の解決方法を紹介しようと思います。

# 解決方法
```diff_swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Menu {
                Button("ボタン1") { }
                Button("ボタン2") { }
                Button("ボタン3") { }
                Button("ボタン4") { }
                Button("ボタン5") { }
            } label: {
                Text("メニューボタン")
            }
+           .menuOrder(.fixed)
            Spacer()
            Menu {
                Button("ボタン1") { }
                Button("ボタン2") { }
                Button("ボタン3") { }
                Button("ボタン4") { }
                Button("ボタン5") { }
            } label: {
                Text("メニューボタン")
            }
+           .menuOrder(.fixed)
        }
    }
}
```

|||
|-|-|
|![スクリーンショット 2022-11-26 22.12.25.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/e5e64f60-e366-a254-8060-93a12c5c4998.png)|![スクリーンショット 2022-11-26 22.12.15.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/eca86e79-4b6d-b726-f33f-b1244d71d789.png)|

# おわり
iOS16からしか使えないです😭

https://developer.apple.com/documentation/swiftui/grid/menuorder(_:)
