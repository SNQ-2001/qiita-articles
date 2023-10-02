---
title: 【SwiftUI】Menuに赤いボタンを追加する
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-10-02T14:21:05+09:00'
id: d3784a3495faa7d0214a
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
SwiftUIのMenu内に「削除」ボタンを実装しようとした時に、
削除ボタンの色は赤くしたかったのでtintやforgroundStyleなどで色変更しようとしてもできなかったので方法を記録しておきます。

# 実装
Buttonのルールを`.destructive`にするとボタンが赤くなります
```swift
Menu {
    Button(role: .destructive) {
        // 処理
    } label: {
        Label("削除", systemImage: "trash")
    }
} label: {
    Image(systemName: "ellipsis")
}
.foregroundStyle(.secondary)
```

# ダメな例
```swift
Menu {
    Button {
        // 処理
    } label: {
        Label("削除", systemImage: "trash")
    }
    .foregroundStyle(.red)
} label: {
    Image(systemName: "ellipsis")
}
.foregroundStyle(.secondary)
```

```swift
Menu {
    Button {
        // 処理
    } label: {
        Label("削除", systemImage: "trash")
    }
    .tint(.red)
} label: {
    Image(systemName: "ellipsis")
}
.foregroundStyle(.secondary)
```

# おわり
ハマりました
