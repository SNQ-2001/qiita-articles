---
title: 【SwiftUI】TabViewに通知バッジを付ける
tags:
  - iOS
  - Swift
  - SwiftUI
  - TabView
private: false
updated_at: '2023-06-19T21:17:12+09:00'
id: ee3b9efde71cf4f66d3c
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
iOS15からTabViewにバッジを付けられるようになりました。

# サンプルアプリ
![simulator_screenshot_192A3CD9-4C2B-41E0-827D-07398BD5BA87.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0db03b31-97e8-35f3-60a4-52c095d561a7.png)

# 実装
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        TabView {
            Text("1st")
                .tabItem {
                    Label("1st", systemImage: "1.circle")
                }
                .badge(30)
            
            Text("2nd")
                .tabItem {
                    Label("2nd", systemImage: "2.circle")
                }
                .badge(100)
            
            Text("3rd")
                .tabItem {
                    Label("3rd", systemImage: "3.circle")
                }
                .badge(50)
        }
    }
}
```

# おわり
iOS14以前までこれができないのきついですね
まぁでももうiOS14は切ってもいいかもしれないですね
