---
title: Makefileの使い方
tags:
  - Makefile
private: false
updated_at: '2023-02-02T21:04:00+09:00'
id: b9a26be2af42a52ca8ff
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
チーム開発をする際に事前にセットアップを行わないといけないことがあり、Makefileを使用したので記録しておきます。

今回の例ではStableDiffusionのモデルをsetup.pyで生成しています。

https://qiita.com/SNQ-2001/items/2d33dc535cf106189f75

# 書き方
```Makefile
.PHONY: setup
setup:
	pip3 install huggingface_hub
	python3 setup.py
	open sample.xcodeproj
```

# 実行方法
```:コマンド
make setup
```

# おわり
`.PHONY`を追加することで複数定義することができます。
