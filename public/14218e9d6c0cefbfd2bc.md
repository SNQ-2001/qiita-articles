---
title: 【SwiftUI】Styleの指定方法を簡潔にする
tags:
  - iOS
  - style
  - Swift
  - SwiftUI
private: false
updated_at: '2022-12-26T20:24:02+09:00'
id: 14218e9d6c0cefbfd2bc
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
SwiftUIはUIコンポーネントにスタイルが指定できるようになっています。
そんなスタイルには指定方法が2つあります。
TabViewのPageスタイルを例に挙げてみます。
以下の2つの指定方法が考えられます。

```swift
TabView {
    Text("タブ1")
    Text("タブ2")
    Text("タブ3")
}
.tabViewStyle(PageTabViewStyle())
```
```swift
TabView {
    Text("タブ1")
    Text("タブ2")
    Text("タブ3")
}
.tabViewStyle(.page)
```

これらは同じ動きをします。
比べてみると下の方が簡潔に書けていると思います。

今回は`.page`のようにカスタムスタイルを指定できるようにする方法を紹介します。

# サンプルアプリ
システム設定のようなリストを作成してみようと思います。
![IMG_1867](https://user-images.githubusercontent.com/84154073/209542692-8a40ca05-34f3-4649-b18d-69edc2e0b725.jpg)


# 実装
### 引数なし
以下のような`LabelStyle`を作成しました。
```swift
struct SystemLabelStyle: LabelStyle {
    func makeBody(configuration: Configuration) -> some View {
        HStack(spacing: 20) {
            configuration.icon
                .frame(width: 30, height: 30)
                .background(Color.gray)
                .foregroundColor(.white)
                .cornerRadius(5)
            configuration.title
                .foregroundColor(.primary)
        }
    }
}
```
引数がない場合はプロパティで指定することができます。
```swift
extension LabelStyle where Self == SystemLabelStyle {
    static var system: SystemLabelStyle {
        .init()
    }
}
```
以下のように使用することができます。
```swift
struct ContentView: View {
    var body: some View {
        List {
            Label {
                Text("一般")
            } icon: {
                Image(systemName: "gear")
            }
            .labelStyle(.system)

            Label {
                Text("コントロールセンター")
            } icon: {
                Image(systemName: "switch.2")
            }
            .labelStyle(.system)
        }
    }
}
```
<img width="257" alt="スクリーンショット 2022-12-26 20 15 14" src="https://user-images.githubusercontent.com/84154073/209542849-ca6d33cd-4151-49f5-9e6e-23ce304ab66e.png">

### 引数あり
先ほどのように背景色がグレーしかない場合はプロパティーで大丈夫です。
しかし、背景色は複数あります。
背景色を指定できるように`LabelStyle`を変更します。
```swift
struct SystemLabelStyle: LabelStyle {
    let color: Color
    func makeBody(configuration: Configuration) -> some View {
        HStack(spacing: 20) {
            configuration.icon
                .frame(width: 30, height: 30)
                .background(color)
                .foregroundColor(.white)
                .cornerRadius(5)
            configuration.title
                .foregroundColor(.primary)
        }
    }
}
```
引数がある場合はメソッドを使用します。
```swift
extension LabelStyle where Self == SystemLabelStyle {
    static func system(color: Color) -> SystemLabelStyle {
        .init(color: color)
    }
}
```
以下のように使用することができます。
```swift
struct ContentView: View {
    var body: some View {
        List {
            Label {
                Text("一般")
            } icon: {
                Image(systemName: "gear")
            }
            .labelStyle(.system(color: .gray))

            Label {
                Text("コントロールセンター")
            } icon: {
                Image(systemName: "switch.2")
            }
            .labelStyle(.system(color: .gray))

            Label {
                Text("画面表示と明るさ")
            } icon: {
                Image(systemName: "textformat.size")
            }
            .labelStyle(.system(color: .blue))
        }
    }
}
```
<img width="257" alt="スクリーンショット 2022-12-26 20 19 56" src="https://user-images.githubusercontent.com/84154073/209543270-88284bbf-fca5-4058-b3f5-f8ecdd63e8a7.png">

# おわり
どちらも使用することができますが、`SystemLabelStyle()`で指定するのは良くない気がします。
```swift
Label {
    Text("一般")
} icon: {
    Image(systemName: "gear")
}
.labelStyle(SystemLabelStyle())
```
```swift
Label {
    Text("コントロールセンター")
} icon: {
    Image(systemName: "switch.2")
}
.labelStyle(.system)
```
