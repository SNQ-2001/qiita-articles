---
title: 【SwiftUI】iOS16で追加されたTableを使ってみた
tags:
  - iOS
  - table
  - Swift
  - SwiftUI
private: false
updated_at: '2022-11-28T21:49:55+09:00'
id: 61ffa7afced1fe0d58f7
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
iOS16でTableとTableColumnという機能が追加されていました。
気になったので使ってみました。

# 完成形
![simulator_screenshot_49C9D741-D7CB-4689-A43A-09F424546461.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/a8f4a4be-793e-ebfb-b724-5f3d3259a7d8.png)

# 今回使用するModel
```swift
struct SoccerPlayer: Identifiable {
    let id = UUID()
    let name: String
    let age: Int
    let position: SoccerPosition
}

enum SoccerPosition: String {
    case gk = "GK"
    case df = "DF"
    case mf = "MF"
    case fw = "FW"
}
```

# 今回使用するデータ
```swift
let players: [SoccerPlayer] = [
    .init(name: "メッシ", age: 35, position: .fw),
    .init(name: "エンバペ", age: 23, position: .fw),
    .init(name: "ネイマール", age: 30, position: .fw),
    .init(name: "ハリー・ケイン", age: 29, position: .fw),
    .init(name: "レヴァンドフスキ", age: 34, position: .fw),
    .init(name: "モドリッチ", age: 37, position: .mf),
    .init(name: "ロナウド", age: 37, position: .fw),
    .init(name: "スアレス", age: 35, position: .fw),
    .init(name: "ノイアー", age: 36, position: .gk),
    .init(name: "ペドリ", age: 20, position: .mf),
    .init(name: "エリクセン", age: 30, position: .mf)
]
```

# 実装
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Table(players) {
            TableColumn("name") { player in
                Text(player.name)
            }
            TableColumn("age") { player in
                Text("\(player.age)")
            }
            TableColumn("position") { player in
                Text(player.position.rawValue)
            }
        }
    }
}
```

# おわり
iPhoneではListのplainスタイルっぽい表示になります。
[tableStyle](https://developer.apple.com/documentation/swiftui/view/tablestyle(_:))というメソッドがありましたが、
まだスタイルはなかったのでこれからということになりそうです。

iPadとMacで機能するみたいです。
iPhoneでは使えなさそうかな？
