---
title: 【Git】既にリモートにあるファイルをGitの管理下から外す
tags:
  - Git
  - GitHub
private: false
updated_at: '2023-04-02T20:51:18+09:00'
id: 34af7d44f2c41cb8dcef
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
Xcodeを触るたびに変化が加わってしまう、厄介なファイルがあったので管理下から外して今後コミットしないようにしました。記録しておきます

# やりかた
`git rm --cached`で管理下から外す
```:ターミナル
git rm --cached /Users/miyamototaishin/Desktop/G-Search/TwitterSearch.xcodeproj/xcuserdata/miyamototaishin.xcuserdatad/xcschemes/xcschememanagement.plist
```

.gitignoreにファイル名を追加して今後コミットしないようにする
```:.gitignore
xcschememanagement.plist
```

.gitignoreをコミット&プッシュする
```:ターミナル
git add .gitignore
git commit -m 'add: .gitignore'
git push origin main
```

# おわり
gitはむずいですね
