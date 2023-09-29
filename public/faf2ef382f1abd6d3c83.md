---
title: 【Swift】アプリがバックグラウンドからフォアグラウンドに切り替わった事を検知する
tags:
  - iOS
  - NotificationCenter
  - UIKit
  - Swift
private: false
updated_at: '2022-09-06T20:20:23+09:00'
id: faf2ef382f1abd6d3c83
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
フォアグラウンドになった事を判定することがあったので記事に残しておきます。

# 実装
```swift
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()

        NotificationCenter.default.addObserver(
            self,
            selector: #selector(foreground),
            name: UIApplication.willEnterForegroundNotification,
            object: nil
        )

    }
    
    @objc func foreground() {
        print("フォアグラウンド")
    }
}
```

# おわり
`NotificationCenter`を有効活用できたらできることの幅が広がりそうなので今度調べてみようと思います。
