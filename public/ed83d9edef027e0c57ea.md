---
title: 【SwiftUI】キーボードショートカットでボタンアクションを実行する
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-08-12T22:00:01+09:00'
id: ed83d9edef027e0c57ea
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
macアプリでボタンにキーボードショートカットをつける機会があったので方法を記録しておきます。

# 実装
以下の実装の場合は`Command` + `q`でボタンのアクションが実行されます。
```diff_swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Button {
            exit(0)
        } label: {
            Text("強制終了")
        }
+       .keyboardShortcut("q")
    }
}
```

# おわり
便利なのでキーボードショートカットは実装しておきたいです
