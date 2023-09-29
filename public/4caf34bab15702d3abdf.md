---
title: 【SwiftUI】@FocusStateを子Viewに渡す
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-06-26T20:26:43+09:00'
id: 4caf34bab15702d3abdf
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
`@FocusState`を子Viewに渡して使うときの方法がちょっと特殊だったので記録しておきます。

# 実装
### 親View
```diff_swift
struct ContentView: View {
    @State private var text: String = ""

+   @FocusState private var focused: Bool

    var body: some View {
        VStack(spacing: 50) {
+           SubView(text: $text, focused: $focused)
            
            Button {
                focused.toggle()
            } label: {
                Text("切り替え")
            }
        }
        .padding(20)
    }
}
```

### 子View
```diff_swift
struct SubView: View {
+   @Binding var text: String
    
    var focused: FocusState<Bool>.Binding

    var body: some View {
        TextField("", text: $text)
+           .focused(focused.projectedValue, equals: true)
            .textFieldStyle(.roundedBorder)
    }
}
```

# 参考記事
https://stackoverflow.com/questions/70141230/passing-down-focusstate-to-another-view

# おわり
初知りでした
