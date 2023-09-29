---
title: 【Git】ブランチを切り替えられない
tags:
  - Git
  - GitHub
  - branch
  - checkout
private: false
updated_at: '2022-07-06T17:09:31+09:00'
id: ffe59ffb081ec3f5ff8c
organization_url_name: null
slide: false
ignorePublish: false
---
# エラー文
```
Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.
```
![スクリーンショット 2022-07-06 13.24.09.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/f5f1ad13-ff47-41ee-10e0-1e598600e5ab.png)

# 解決方法
`index.lock`を削除します。
![スクリーンショット 2022-07-06 13.27.43.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/6795c561-28ae-345a-bbe4-de79b3d4ddc1.png)

# 参考

https://stackoverflow.com/questions/38004148/another-git-process-seems-to-be-running-in-this-repository
