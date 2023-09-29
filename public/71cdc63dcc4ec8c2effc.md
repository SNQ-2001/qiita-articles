---
title: 【SwiftUI】DisclosureGroupを使ってみた
tags:
  - iOS
  - Swift
  - SwiftUI
  - DisclosureGroup
private: false
updated_at: '2022-10-26T13:02:39+09:00'
id: 71cdc63dcc4ec8c2effc
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
iOS14で追加された`DisclosureGroup`を初めて触ってみたので記録しておきます。

# どんな動きをするものなの？
![Simulator Screen Recording - iPhone 14 Pro - 2022-10-24 at 19.09.35.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/72226f8f-0ba4-fa41-3b1a-fd419737240e.gif)

# 実装
`DisclosureGroup`でネストしていく感じですね。
とてもわかりやすいです。
```swift
import SwiftUI

struct ContentView: View {
    @State var sliderValue: CGFloat = 50.0
    var body: some View {
        List {
            DisclosureGroup("メニュー") {
                DisclosureGroup("朝ごはん") {
                    Text("納豆ごはん")
                    Text("味噌汁")
                    Text("焼き魚")
                }
                DisclosureGroup("昼ごはん") {
                    Text("ラーメン")
                }
                DisclosureGroup("夜ごはん") {
                    Text("白米")
                    Text("チキンソテー")
                    Text("トマトスープ")
                    Text("キャベツのサラダ")
                }
            }
        }
    }
}
```

### コードで開閉する
`isExpanded`を使用することでコードで開閉ができる
```swift
DisclosureGroup("メニュー", isExpanded: $isShow) {
    Text("")
}
```

# おわり
いままで1回も使ったことがなかったので今回触れることができてよかったです。


でもこれあんまり使いどころないよな。。。
