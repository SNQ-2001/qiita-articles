---
title: 【UIKit】指定した色と違う色がNavigationBarに表示される
tags:
  - iOS
  - UIKit
  - Swift
private: false
updated_at: '2022-07-10T22:14:59+09:00'
id: aa1fc4cd14aa5ca7d38b
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
UIKitは学び始めたばかりなので間違っていたり、もっと良い方法がある可能性があります。
そのような場合はコメントか編集リクエストを送ってください。

# やろうとしている事
こちらの画像をナビゲーションバーに表示して、
画像の背景と同じ色をナビゲーションバーに表示したい。
![logo-background-color.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/75c64834-258f-d210-2a21-9b16ed8a5622.png)

# 作業
まず、画像の背景のRGBを調べます。
![スクリーンショット 2022-07-09 18.35.55.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/46430dab-41d5-f19f-7b24-b03944e79999.png)

`rgb(85,197,0)`でした。
このRGBをナビゲーションバーに設定します
```swift
import UIKit

class NavigationViewController: UINavigationController {
    override func viewDidLoad() {
        super.viewDidLoad()
        navigationBar.barTintColor = UIColor(red: 85/255, green: 197/255, blue: 0/255, alpha: 1.0)
    }
}
```
続いて、ナビゲーションバーに画像を配置します。
```swift
import UIKit

class TabBarViewController: UITabBarController {
    var qiita: UIImageView = {
        let view = UIImageView(image: UIImage(named: "logo-background-color"))
        view.translatesAutoresizingMaskIntoConstraints = false
        view.contentMode = .scaleAspectFit
        return view
    }()
    override func viewDidLoad() {
        super.viewDidLoad()
        navigationItem.titleView = qiita
    }
}
```

これで完成です
ビルドしてみましょう
![Simulator Screen Shot - iPhone 12 - 2022-07-09 at 18.39.25.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/b6f7f496-bbcb-0cb6-7467-7e3b1fc2eff6.png)

あれ？なんで？
もしかしたらRBGサイトがおかしかったのかもしれません。
ビルド後のスクショでRGBを見てみましょう

![スクリーンショット 2022-07-09 18.43.26.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/f6a53191-d864-b369-7d77-a172759948f2.png)

ナビゲーションバーの色は`rgb(110,206,32)`だそうです。
これおかしいのサイトじゃなくてナビゲーションバーじゃない？
もしかして`UIColor(red:, green:, blue:, alpha:)`がバグってる？

しかし、ナビゲーションバー以外では正常に表示されます。

じゃあナビゲーションバーがおかしいじゃんという事になります。

# 原因は？
![Simulator Screen Shot - iPhone 12 - 2022-07-09 at 18.48.56.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/33b4fee0-fb09-696a-0774-4a83de691d1a.png)
これは推測ですが、
上の画像のようにナビゲーションバーにはデフォルトでグレーっぽい色がついています。
これの上に色を乗せているので指定した色と違う色が表示されているのではないでしょうか。

# 解決方法
```diff_swift
import UIKit

class NavigationViewController: UINavigationController {
    override func viewDidLoad() {
        super.viewDidLoad()

-       navigationBar.barTintColor = UIColor(red: 85/255, green: 197/255, blue: 0/255, alpha: 1.0)

+       let appearance = UINavigationBarAppearance()
+       appearance.backgroundColor = UIColor(red: 85/255, green: 197/255, blue: 0/255, alpha: 1.0)
+       UINavigationBar.appearance().standardAppearance = appearance
+       UINavigationBar.appearance().compactAppearance = appearance
+       UINavigationBar.appearance().scrollEdgeAppearance = appearance

    }
}
```
![Simulator Screen Shot - iPhone 12 - 2022-07-09 at 18.55.04.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1f14be0e-2347-9abf-3a58-bf5b45c6dd5a.png)
このようになりました。
完璧ですね

# おわり
これはバグなのか、仕様なのか
もしかしたらナビゲーションバーの色の変え方が適切ではない可能性？？
