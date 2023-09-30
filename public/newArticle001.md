---
title: 【XcodeCloud】XcodeCloudで実行した時はBuildPhasesのRunScriptを実行したくない
tags:
  - ''
private: false
updated_at: ''
id: null
organization_url_name: null
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