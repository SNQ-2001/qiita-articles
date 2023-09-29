---
title: 【SwiftUI】特定の条件でのみオーバーレイする
tags:
  - Xcode
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-01-21T21:37:33+09:00'
id: cbbe13f40a1dfe8eaff4
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
条件によって`Text("Hello, world!")`にオーバーレイの有無を決定したいとします。

# サンプルアプリ
![Simulator Screen Recording - iPhone 14 Pro - 2023-01-21 at 21.35.26.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/8039a8ff-ea86-d602-c248-ec9f0ac3dc15.gif)


# やりかた
```swift:ContentView
import SwiftUI

struct ContentView: View {
    @State var isShowBorder: Bool = false
    var body: some View {
        VStack(spacing: 50) {
            Toggle("", isOn: $isShowBorder)
                .labelsHidden()

            Text("Hello, world!")
                .padding(.init(top: 10, leading: 20, bottom: 10, trailing: 20))
                .overlay(isOverlay: isShowBorder) {
                    RoundedRectangle(cornerRadius: 10).stroke(style: .init(lineWidth: 3))
                }
        }
    }
}
```
```swift:View+
import SwiftUI

extension View {
    @ViewBuilder
    func overlay<T: View>(isOverlay: Bool, content: () -> T) -> some View {
        if isOverlay {
            self.overlay {
                content()
            }
        } else {
            self
        }
    }
}
```

ここで重要なのは`@ViewBuilder`です。

# おわり
久しぶりにSwiftUIの記事を書きました
