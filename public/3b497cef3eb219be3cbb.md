---
title: 【Swift】TCAで2つのActionを同時に実行する
tags:
  - iOS
  - Swift
  - TCA
private: false
updated_at: '2023-08-26T22:19:39+09:00'
id: 3b497cef3eb219be3cbb
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
TCAを使っていて同時にアクションを実行したい場面がありました。
やり方を知ったので記録しておきます。

# 実装
```diff_swift
import SwiftUI
import ComposableArchitecture

struct ContentView: View {
    @ObservedObject private var viewStore: ViewStoreOf<Feature>
    
    let store: StoreOf<Feature>
    
    init(store: StoreOf<Feature>) {
        self.store = store
        self.viewStore = ViewStore(store, observe: { $0 })
    }

    var body: some View {
        Button {
            viewStore.send(.buttonTapped)
        } label: {
            Text("テスト")
        }
    }
}

struct Feature: Reducer {
    struct State: Equatable {}

    enum Action: Equatable {
        case buttonTapped
        case printA
        case printB
    }
    
    func reduce(into state: inout State, action: Action) -> Effect<Action> {
        switch action {
        case .buttonTapped:
+           return .concatenate(.send(.printA), .send(.printB))
        case .printA:
            print("A")
            return .none
        case .printB:
            print("B")
            return .none
        }
    }
}
```

# おわり
TCAの知見ためていきたいです
