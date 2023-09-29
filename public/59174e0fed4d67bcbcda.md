---
title: 【Xcode】新しいSFSymbolでも全てのOSバージョンで使いたい
tags:
  - Xcode
  - iOS
  - Swift
  - SFSymbols
private: false
updated_at: '2023-01-03T22:20:51+09:00'
id: 59174e0fed4d67bcbcda
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
「うわ！めっちゃ欲しかったSFSymbolsが追加されてるじゃん！使お」
「まじか、iOS16.1からしか使えないじゃん」

こんな経験ありますよね

大丈夫、使えるんです

# やりかた
① 使いたいシンボルを選択します
② 「ファイル」を選択します
③ 「シンボルを書き出す...」を選択します
![スクリーンショット 2023-01-03 22.05.40.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/e1c3425e-7664-67c8-b355-7d186d2ba31a.png)

④ 「書き出す」を選択します
![スクリーンショット 2023-01-03 22.08.21.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/3001404c-3bbc-04fd-c951-4ad427896cb1.png)

⑤ ファイル名を決めます
⑥ 保存場所を決めます
⑦ 「書き出す」を選択します
![スクリーンショット 2023-01-03 22.12.40.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/7f6c1c4e-6d1a-456b-9429-bdead7c4e9f0.png)

⑧ Assetsを選択します
⑨ 先ほど書き出したファイルをAssets内にドラッグします
![スクリーンショット 2023-01-03 22.15.48.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/491ebd5a-20df-c2d9-cc1c-b4ae4a5fcaeb.png)

# 使い方
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Image("sos")
    }
}
```

# おわり
iOS14でも使うことができました
![simulator_screenshot_F17EEEDB-ECED-4EBA-ADC5-AEB5E54E5E9E.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/0aaeebe9-b069-1d99-513c-13ef850adcd9.png)
