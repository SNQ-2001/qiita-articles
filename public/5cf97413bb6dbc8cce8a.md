---
title: 【SwiftUI】強制アップデートアラートを表示させる
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-02-24T22:09:44+09:00'
id: 5cf97413bb6dbc8cce8a
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
ユーザーには最新のバージョンを使って欲しいです。
ですのでAppStoreに最新バージョンがリリースされたらアプリに通知します。
よく使う機能なのでライブラリを作成しました。

作成したライブラリの使い方を紹介します。

https://github.com/SNQ-2001/AppVersionMonitorSwiftUI

# サンプルアプリ
![simulator_screenshot_6CF8E9C7-F238-466D-B211-4AD971938E03.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/035c9151-0dc1-51f6-e277-a5f03a7294b6.png)

# ライブラリの導入
① 「File」を選択します
② 「Add Packages...」を選択します
![スクリーンショット 2023-02-24 21.36.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/d2d37573-24f3-ecfb-6fbd-bde65ea4d815.png)

③ `https://github.com/SNQ-2001/AppVersionMonitorSwiftUI`を検索します
④ 「Up to Next Major Version」を選択します
⑤ 「Add Package」を選択します
![スクリーンショット 2023-02-24 21.39.58.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/e49db481-dab1-de09-1326-2adfc071c323.png)

⑥ 「Add Package」を選択します
![スクリーンショット 2023-02-24 21.43.06.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/fb9a67c9-e9e9-2eba-7510-68be87dbd1b7.png)

# 実装
```swift
import SwiftUI
import AppVersionMonitorSwiftUI

struct ContentView: View {
    @State var isAlert: Bool = false
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundColor(.accentColor)
            Text("Hello, world!")
        }
        .alert(isPresented: $isAlert) {
            Alert(title: Text("お知らせ"), message: Text("最新バージョンがあります"), dismissButton: .default(Text("OK")) {
                // TODO: ここでAppStoreを開く
            })
        }
        .appVersionMonitor(id: 1570395606) { status in
            switch status {
            case .updateAvailable:
                isAlert = true
                print("アップデートがあります")
            case .updateUnavailable:
                print("アップデートがありません")
            case .failure(let error):
                print("エラーが発生しました: \(error)")
            }
        }
    }
}
```

# アプリIDについて
`id`でしている数字はアプリIDです。
```swift
.appVersionMonitor(id: 1570395606) { status in
```
アプリIDはAppStoreのURLで確認できます。
```url
https://apps.apple.com/jp/app/g-search/id1570395606
```
後ろについている数字が`id`です。

リリース前のアプリのアプリIDを知る方法は別記事で紹介しています。

https://qiita.com/SNQ-2001/items/df93fc0804666a8c3263

# 注意事項
アプリバージョンの指定方法は「Semantic Versioning 2.0.0」を採用しています。

例：`1.0.0` `2.1.3` `3.10.1`

「Semantic Versioning 2.0.0」以外のバージョンの指定方法は使用できません。

「Semantic Versioning 2.0.0」については、以下の記事がわかりやすかったです。

https://qiita.com/usamik26/items/c8911219b610101e69a9

# おわり
スターください！
IssueやPRもお願いします！

https://github.com/SNQ-2001/AppVersionMonitorSwiftUI
