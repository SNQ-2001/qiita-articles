---
title: 【SwiftUI】点線の枠線をつける
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-08-20T22:10:37+09:00'
id: a9ea20a85fcde2f9d5db
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
![simulator_screenshot_94C3A659-28C7-4BF3-B798-057360E5CF18.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/2cdeebeb-cef5-726b-7333-72984575fdb3.png)

# 実装
```diff_swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("点線の枠線")
            .frame(width: 180, height: 60)
+           .overlay(.black, in: RoundedRectangle(cornerRadius: 10).stroke(style: .init(lineWidth: 2, dash: [2, 4])))
    }
}
```

# おわり
割と簡単に実装できました
