---
title: 【SwiftUI】レトロスタイルを実装してみた
tags:
  - Design
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2022-12-28T19:40:29+09:00'
id: 0beecfab39ebf8336c84
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
[こちら](https://appmaster.io/ja/blog/2022nian-nomobairuapuriuidezainnoaideatotsupu10)のサイトを見ていたら90年代のスタイルがイケてたのでSwiftUIで再現してみました。
![appmaster](https://user-images.githubusercontent.com/84154073/209798974-add7bf62-234a-46b3-a215-4852594bec61.png)

# サンプルアプリ
![Simulator Screen Recording - iPhone 14 Pro - 2022-12-28 at 19 37 47](https://user-images.githubusercontent.com/84154073/209799326-ffa20435-8047-41e1-9735-0ec843263049.gif)

# 実装
```swift:ContentView
import SwiftUI

struct ContentView: View {
    @State var text: String = ""
    var body: some View {
        VStack(spacing: 30) {
            Button {
                print()
            } label: {
                Text(text)
                    .font(.system(size: 30, weight: .black, design: .rounded))
                    .frame(maxWidth: .infinity, minHeight: 200)
                    .padding()
            }
            .buttonStyle(.retro(borderLineWidth: 10))

            LazyVGrid(columns: Array(repeating: .init(.flexible(), spacing: 30), count: 4), spacing: 20) {
                ForEach(0..<20, id: \.self) { index in
                    Button {
                        text += index.description
                    } label: {
                        Text("\(index)")
                            .font(.system(size: 30, weight: .black, design: .rounded))
                            .frame(width: 60, height: 60)
                    }
                    .buttonStyle(.retro(borderLineWidth: 5))
                }
            }

            Button {
                text = ""
            } label: {
                Text("Clear")
                    .font(.system(size: 30, weight: .black, design: .rounded))
                    .frame(maxWidth: .infinity, minHeight: 20)
                    .padding()
            }
            .buttonStyle(.retro(borderLineWidth: 5))
        }
        .padding(.horizontal, 30)
    }
}
```

```swift:RetroButtonStyle
struct RetroButtonStyle: ButtonStyle {
    let borderLineWidth: CGFloat
    func makeBody(configuration: Configuration) -> some View {
        configuration.label
            .background(.white, in: RoundedRectangle(cornerRadius: 10))
            .compositingGroup()
            .shadow(color: .black, radius: 0, x: borderLineWidth, y: borderLineWidth)
            .overlay(.black, in: RoundedRectangle(cornerRadius: 10).stroke(style: .init(lineWidth: borderLineWidth)))
            .scaleEffect(configuration.isPressed ? 1 : 0.99)
    }
}

extension ButtonStyle where Self == RetroButtonStyle {
    static func retro(borderLineWidth: CGFloat) -> RetroButtonStyle {
        .init(borderLineWidth: borderLineWidth)
    }
}
```

# おわり
デザインは奥が深いですね
ゼンリーのデザイン好きだったのに無くなるの悲しい。。。
