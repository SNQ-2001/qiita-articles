---
title: 【TCA】@BindingStateを使って値を監視する
tags:
  - iOS
  - Swift
  - TCA
  - SwiftUI
private: false
updated_at: '2023-09-15T20:06:27+09:00'
id: 8afeeb7c45e2dff91d0f
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
@BindingStateの使い方を記録しておきます

# 完成
![画面収録-2023-09-15-19.59.47.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/920c9395-67a6-67f5-da04-c8a74c04e617.gif)

# 実装
### Reducer
```diff_swift
import Foundation
import ComposableArchitecture

public struct SampleReducer: Reducer {
    public init() {}

    // MARK: - State
    public struct State: Equatable {
+       @BindingState var text = "" // @BindingStateを付与
        
        public init() {}
    }

    // MARK: - Action
+   public enum Action: BindableAction, Equatable { // `BindableAction`に準拠させる
+       case binding(BindingAction<State>)
    }

    // MARK: - Reducer
    public var body: some ReducerOf<Self> {
+       BindingReducer() // ここが重要
        
        Reduce { state, action in
            switch action {
+           case .binding(\.$text):  // ここにtextの変更が流れてくる
+               print("変更:", state.text)
+               return .none
+           case .binding: // ここはその他の`binding`が流れてくる(今回はなし)
+               return .none
            }
        }
    }
}
```

### View
```swift
import SwiftUI

struct ContentView: View {
    @ObservedObject private var viewStore: ViewStoreOf<SampleReducer>
    
    let store: StoreOf<SampleReducer>
    
    init(store: StoreOf<SampleReducer>) {
        self.store = store
        self.viewStore = ViewStore(store, observe: { $0 })
    }
    
    var body: some View {
        VStack {
            TextField("search", text: viewStore.$text) // 使う時は`$`を付ける
                .textFieldStyle(.roundedBorder)
        }
        .padding(.horizontal, 20)
    }
}
```

# おわり
TCAめっちゃむずいです
