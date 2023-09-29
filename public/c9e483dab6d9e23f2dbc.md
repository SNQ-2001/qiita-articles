---
title: 【Swift】for文内のif文を省略できるらしい
tags:
  - Xcode
  - iOS
  - Swift
private: false
updated_at: '2022-11-03T21:07:01+09:00'
id: c9e483dab6d9e23f2dbc
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
SwiftLintを使ってたら警告が表示されて気づいたのですが、for文内のif文は`where`を使って1文にできるらしいです。

# やりかた
```swift
for user in users {
    if user == "SNQ-2001" {
        print("自分です")
    }
}
```

```swift
for user in users where user == "SNQ-2001" {
    print("自分です")
}
```

# おわり
こういうコードの省略形みたいなの知るとめっちゃ嬉しくなっちゃいます笑
