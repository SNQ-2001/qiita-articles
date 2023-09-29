---
title: 【Swift】SwiftGenをSwiftPMで管理する
tags:
  - Xcode
  - iOS
  - Swift
  - Swiftgen
  - SwiftPM
private: false
updated_at: '2023-01-16T19:51:46+09:00'
id: 8ddf4e9ecbfe25dc82cd
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
https://qiita.com/SNQ-2001/items/c56658193d54c040c1fb

https://qiita.com/SNQ-2001/items/e202893e37898bb0c721

https://qiita.com/SNQ-2001/items/b2ea9cd49238db352f5c

これまでSwiftFormat、SwiftLint、LicensePlistをSwiftPMで管理する方法を記事にしてきました。
今回はSwiftGenをSwiftPMで管理してみます。

「swiftpm-swiftgen」というプロジェクトを作成しました。

![スクリーンショット 2023-01-16 16.56.15.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/bf98e948-7874-37af-9698-ce79b66933eb.png)

# やりかた
swiftpm-swiftgenに移動します。
```:ターミナル
cd /Users/miyamototaishin/Desktop/swiftpm-swiftgen
```
![スクリーンショット 2023-01-16 16.58.14.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/19226c8e-3743-fc51-25da-bd5ecfefdede.png)

BuildToolsというフォルダを作成します。
```:ターミナル
mkdir BuildTools
```
![スクリーンショット 2023-01-16 16.58.55.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/9225389b-e130-1820-bbbe-b26845ebfbcf.png)

BuildToolsに移動します。
```:ターミナル
cd BuildTools
```
![スクリーンショット 2023-01-16 16.59.25.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/8566437a-2a3a-6cf3-654d-1650a039c195.png)

`Package.swift`を作成します。
```:ターミナル
touch Package.swift
```
![スクリーンショット 2023-01-16 17.00.09.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/fc56a4f3-1bc0-5ad3-cb38-f4fe95c4b16b.png)

`Empty.swift`を作成します。
```:ターミナル
touch Empty.swift
```
![スクリーンショット 2023-01-16 17.00.40.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0984a970-b926-b343-c981-1863d2fe354f.png)

`Package.swift`を開きます。
```:ターミナル
open Package.swift
```
![スクリーンショット 2023-01-16 17.01.13.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/451ae79c-4b48-e82e-eabf-4f64fd27e1b0.png)

`Package.swift`に以下をコピペします。
```Package.swift
// swift-tools-version: 5.6
import PackageDescription

let package = Package(
    name: "BuildTools",
    dependencies: [
        .package(url: "https://github.com/SwiftGen/SwiftGen", from: "6.0.0")
    ],
    targets: [.target(name: "BuildTools", path: "")]
)
```

ディレクトリを１つ上の階層に移動します。
```:ターミナル
cd ..
```
![スクリーンショット 2023-01-16 17.38.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/aed1509d-6f5d-8a7b-c359-d0b0edce5e8e.png)


`swiftgen.yml`を作成します。
```:ターミナル
touch swiftgen.yml
```
![スクリーンショット 2023-01-16 17.45.21.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0918411b-a7db-ea80-1cad-c07b1a380af2.png)

`swiftgen.yml`を開きます。
```:ターミナル
open swiftgen.yml
```
![スクリーンショット 2023-01-16 17.46.12.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/7285d380-5bda-ce12-9ca7-bb95baca8918.png)

`swiftgen.yml`を編集します。
ここの編集は各々設定をお願いします。
```swiftgen.yml
xcassets:
  inputs:
    - ${TARGET_NAME}/Assets.xcassets
  outputs:
    - templateName: swift5
      output: ${TARGET_NAME}/Assets.swift
```

### Run Scriptを作成
プロジェクトをダブルタップで開きます。
![スクリーンショット 2023-01-16 17.48.57.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/ae2aafb9-f746-84e5-433c-3a2e6c8bbd87.png)

① プロジェクトを選択します
② ターゲットを選択します
③ 「Build Phases」を選択します
④ 「+」を選択します
![スクリーンショット 2023-01-16 17.49.50.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/f6c541c7-1b71-18ee-1e8f-e994f2a7fa93.png)

⑤ 「New Run Script Phase」を選択します
![スクリーンショット 2023-01-16 17.51.07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/ea1dc06d-b394-1179-7841-d7d611f7ccae.png)

追加された「Run Script」に以下のスクリプトをコピペします。
```sh
cd BuildTools

xcrun --sdk macosx swift build -c release
```
![スクリーンショット 2023-01-15 20.47.02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1c06f195-e643-c73b-79d5-b3acd3f5ef23.png)

先ほどと同じ手順でRun Scriptを作成します。
作成したRun Scriptに以下のスクリプトをコピペします。

```sh
cd BuildTools

xcrun --sdk macosx swift build -c release \
--package-path .build/checkouts/SwiftGen \
--product swiftgen

.build/checkouts/SwiftGen/.build/release/swiftgen config run --config $SRCROOT/swiftgen.yml
```
![スクリーンショット 2023-01-16 19.41.24.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/8d3712f1-eea3-6354-e5d8-a4d9be522e90.png)

### ビルド
ビルドします。
![スクリーンショット 2023-01-16 19.42.51.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/e9a8ea82-ec31-0f15-3ec3-3ecea39098ea.png)

成功していれば`Assets.swift`が生成されているはずです。
![スクリーンショット 2023-01-16 19.43.48.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/bff7c69f-bbec-7dd7-ec53-6f3844987c99.png)

Xcodeに読み込ませます。
① メインターゲットのフォルダを右クリックします
② 「Add Files to "swiftp,-swiftgen"...」を選択します
![スクリーンショット 2023-01-16 19.45.20.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/e656cdd5-efef-f018-4cb5-717980ac7f4b.png)

③ 生成された`Assets.swift`を選択します
④ 「Add」を選択します
![スクリーンショット 2023-01-16 19.47.34.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/fc40d699-f4e1-af08-a52d-a62438825a91.png)

Xcodeに読み込むことができました。
![スクリーンショット 2023-01-16 19.49.13.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/b2653e99-17c3-ba58-8495-874f1aeeddf3.png)

# おわり
SwiftFormat、SwiftLint、SwiftGen、LicensePlistをSwiftPMで管理できるようになったことによって個人開発ではMintを使用しなくて良くなりました！！
CocoaPodsも卒業できて、Mintも卒業できました！！
