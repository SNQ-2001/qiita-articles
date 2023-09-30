---
title: 【XcodeCloud】XcodeCloudで実行した時はBuildPhasesのRunScriptを実行したくない
tags:
  - Xcode
  - iOS
  - Swift
  - XcodeCloud
private: false
updated_at: '2023-09-30T15:27:04+09:00'
id: 3bdaaee1aefc3b847b32
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
SwiftLintをRunScriptでビルドしてたのですが、XcodeCloudでの実行時間がめっちゃ長くなっちゃうので、
XcodeCloudで実行された時は処理をスキップしたいことがありました。
その時にRunScript上でXcodeCloudで実行されていることを検知する環境変数を知ったので記事にしておきます。

# 実装
```sh
if [ "$CI_XCODE_CLOUD" == "TRUE" ]; then
  echo "✅ XcodeCloudで実行されました"
else
  echo "❌ XcodeCloud以外で実行されました"
fi
```

これを使ってXcodeCloudの時は処理をスキップしたい時はこうなります。

```sh
if [ "$CI_XCODE_CLOUD" == "TRUE" ]; then
    exit 0
fi

# 行いたい処理
```

# おわり
XcodeCloudの実行時間が15分 → 3分に短縮されました！

# ドキュメント
https://developer.apple.com/documentation/xcode/environment-variable-reference
