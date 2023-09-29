---
title: 【Xcode】シュミレーターAppleWatchとシュミレーターiPhoneの紐付け
tags:
  - Xcode
  - Simulator
  - Swift
  - watchOS
private: false
updated_at: '2022-07-22T23:27:18+09:00'
id: c72bca5e8c1eefe9cd29
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr"><a href="https://twitter.com/hashtag/SwiftUI%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E4%B8%80%E6%9C%AC%E5%8B%9D%E8%B2%A0?src=hash&amp;ref_src=twsrc%5Etfw">#SwiftUIレイアウト一本勝負</a> 002<br><br>- ナビゲーション階層による画面遷移を前提としてください（NavigationLink を用いてください）<br>- macOS App は考慮しなくてよいこととします<br>- エンティティ・サンプルデータ の提供があります（リプライを参照、利用は必須ではありません） <a href="https://t.co/VdmBbux8fr">pic.twitter.com/VdmBbux8fr</a></p>&mdash; treastrain / Tanaka.R (@treastrain) <a href="https://twitter.com/treastrain/status/1549595274653609984?ref_src=twsrc%5Etfw">July 20, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

こちらのお題を解いている時に初めてApple Watchをシュミレーターで起動しました。
そこで気づきました。
Apple Watchの言語が英語から変更できない。。。
ここでかなり時間溶けました笑

根本の原因はAppleWatchとiPhoneの関係性がわかっていなかったからだと思います。
今回はシュミレーターのApple WatchをシュミレーターのiPhoneに紐付けする方法を紹介します。

明日はシュミレーターのApple Watchの言語を変更する方法を投稿します。

# 方法
「Window」から「Devices and Simulators」を選択します。
![スクリーンショット 2022-07-22 22.48.12.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/54285ae8-bcbb-fcab-4663-f98bc136f603.png)
今回はiPhone13を使用します。
iPhoneを選択したら「＋」を押します。
![スクリーンショット 2022-07-22 22.51.01.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/3958ef61-e3b2-f135-27dc-630a2082b812.png)
紐付けしたいapple watchの種類を選択したら「Pair」を押します。
![スクリーンショット 2022-07-22 22.55.32.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/67b3fbde-365a-3378-a0eb-da9da218198d.png)
こうなってればOKです。
![スクリーンショット 2022-07-22 22.56.45.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/586469ad-9cb1-bab2-db99-83615fdba17c.png)
紐付けした端末を両方ビルドします。
今回の例では「iPhone13」と「Apple Watch Series7 - 45mm」です。
両方ビルドできたら「Watch」を開いてみましょう。同期が始まります。
![スクリーンショット 2022-07-22 23.05.50.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/ae30f9b3-d67a-3961-20e4-b1ce12d3a866.png)
以下の画像のように表示されていれば、同期は完了です。
![スクリーンショット 2022-07-22 23.12.05.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/4ce6e96d-b968-7e50-95ff-fe0ac201501e.png)

# 完成
![スクリーンショット 2022-07-22 23.13.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/1bfd953d-86d3-9dd9-f4f9-628f3c496fb1.png)

# おわり
watchOSの情報は少ないので沼にハマると一瞬で時間が溶けます笑
