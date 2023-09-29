---
title: 【Swift】UIImageを重ねる
tags:
  - iOS
  - UIKit
  - Swift
private: false
updated_at: '2023-06-24T19:09:14+09:00'
id: a4eccbaa613d1fd41baf
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
SwiftUIはめっちゃ使うんですが、UIKitはなかなか使わないので画像の重ね方が分かりませんでした。
調べたので記事にします。

# 実装
```swift
import UIKit

extension UIImage {
    public func overlay(image: UIImage, width: CGFloat = 100, height: CGFloat = 100) -> UIImage? {
        UIGraphicsBeginImageContextWithOptions(size, false, 0)

        draw(in: CGRect(x: 0, y: 0, width: size.width, height: size.height))

        let rect = CGRect(
            x: (size.width - width) / 2,
            y: (size.height - height) / 2,
            width: width,
            height: height
        )

        image.draw(in: rect)

        let image = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()

        return image
    }
}
```

# 使い方
```swift
UIImage(named: "sample").overlay(image: UIImage(named: "overlay_image"))
```

# おわり
いい感じになりました

# 参考記事
https://faboplatform.github.io/SwiftDocs/1.uikit/060_uiimage/

https://qiita.com/tiqwab/items/846f548416f29b5ae85a

https://qiita.com/ken_sasaki2/items/9a6304e0cd47efddeca1

https://dev.classmethod.jp/articles/swift-generate-qr-code/
