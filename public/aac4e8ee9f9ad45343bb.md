---
title: 【Swift】マルチモジュール構成を試してみた
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-04-11T23:47:57+09:00'
id: aac4e8ee9f9ad45343bb
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
最近、マルチモジュール構成のやり方を知ったので記録しておきます。

# Packageを作成する
① 「File」を選択します
② 「New」を選択します
③ 「Package...」を選択します
![スクリーンショット 2023-04-11 23.19.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/7cf4b7e4-b975-366d-3870-c43c7b0ca96c.png)

④ パッケージ名を入力します(今回はCoreにしました)
![スクリーンショット 2023-04-11 23.22.12.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0d64f9c2-ea83-452f-de00-2cd8bbcb2ff3.png)

⑤ 保存したいディレクトリを選択します
![スクリーンショット 2023-04-11 23.24.21.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0079963d-6ac0-bbd0-b8a9-cbcdc1a7b2ad.png)

⑥ プロジェクトを選択します
⑦ 「Create」を選択します
![スクリーンショット 2023-04-11 23.25.29.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1d3e20dd-f14f-fa8f-507d-def7b598736b.png)

このようになりました。
![スクリーンショット 2023-04-11 23.28.25.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/517be048-ea9f-1b27-c2e1-a0689f736e20.png)

# モジュールを作成する
今回はサンプルとして`APIClient`と`Repository`のモジュールを作成してみようと思います。

① `Core`と`CoreTests`を選択します(コマンド押しながら選択すると複数選択できる)
② 右クリックをして「Delete」を選択します
![スクリーンショット 2023-04-11 23.30.05.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/138225fd-ebaa-662d-a297-a23284a0be27.png)

③ 「Move to Trash」を選択します
![スクリーンショット 2023-04-11 23.31.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/9ae46dfa-5398-3d70-3596-68d86f146422.png)

④ 「Sources」を右クリックします
⑤ 「New Folder」を選択します
![スクリーンショット 2023-04-11 23.34.18.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/65f26bcf-d1ba-e43f-7ab5-9a7a20c922da.png)

⑥ `APIClient`と入力します
![スクリーンショット 2023-04-11 23.36.05.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/c1cf0dce-ca2c-4eea-729d-1f6ecfe2a915.png)

上記の手順であと3つほどフォルダを作成します。
- APIClient
- Repository
- APIClientTests
- RepositoryTests

![スクリーンショット 2023-04-11 23.38.28.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/4899c102-9c55-a723-9c83-f99e477462a2.png)

フォルダ内にファイルがないとエラーになるので適当なファイルを作成します。
![スクリーンショット 2023-04-11 23.43.00.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1d788bd3-35b2-7aa5-5434-3ebcf242270e.png)

# Package.swiftの編集
```Package.swift
import PackageDescription

let package = Package(
    name: "Core",
    products: [
        // Products define the executables and libraries a package produces, and make them visible to other packages.
        .library(
            name: "APIClient",
            targets: ["APIClient"]
        ),
        .library(
            name: "Repository",
            targets: ["Repository"]
        ),
    ],
    dependencies: [
        // Dependencies declare other packages that this package depends on.
        // .package(url: /* package url */, from: "1.0.0"),
    ],
    targets: [
        // Targets are the basic building blocks of a package. A target can define a module or a test suite.
        // Targets can depend on other targets in this package, and on products in packages this package depends on.
        .target(
            name: "APIClient",
            dependencies: []
        ),
        .target(
            name: "Repository",
            dependencies: []
        ),
        .testTarget(
            name: "APIClientTests",
            dependencies: ["APIClient"]
        ),
        .testTarget(
            name: "RepositoryTests",
            dependencies: ["Repository"]
        ),
    ]
)
```

# 使う
このようにインポートできるようになリます。
![スクリーンショット 2023-04-11 23.44.47.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/2bf928fc-e80f-0a93-26db-912b41c0d012.png)

# おわり
さっそく個人開発アプリに導入してみました
