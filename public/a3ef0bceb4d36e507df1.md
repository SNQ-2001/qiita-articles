---
title: 【Swift】プロパティの種類
tags:
  - iOS
  - Swift
  - 演算子
private: false
updated_at: '2023-04-26T21:05:13+09:00'
id: a3ef0bceb4d36e507df1
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
プロパティについてよく理解してなかったので整理しました。

# ストアドプロパティ
```swift:例1
var sample: String = "サンプル"
```

```swift:例2
var sample: String

init(sample: String) {
    self.sample = sample
}
```

# コンピューテッドプロパティ
```swift:例1
var sample: String {
    "sample"
}
```

```swift:例2
var sample: String {
    get {
        return "sample"
    }
    set(newValue) {
        print("new value: \(newValue)")
    }
}
```

```swift:例3
var sample: String = {
   "sample"
}()
```

# おわり
間違っているところがあればコメントで教えていただきたいです。
