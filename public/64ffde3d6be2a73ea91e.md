---
title: 【Swift】classとstructの違いを理解していなかったので整理してみた
tags:
  - iOS
  - Swift
private: false
updated_at: '2023-09-17T20:25:20+09:00'
id: 64ffde3d6be2a73ea91e
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
いままでclassとstructの違いをしっかり調べたことがなかったのでまとめてみました

# 違い1(初期化)
### class
`class`はイニシャライザが必須です。
ないと怒られます
```swift
class PersonClass {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}
```
![スクリーンショット 2023-09-17 19.58.43.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/6420c90a-2d00-8244-ddf0-10759c881dc5.png)

### struct
`struct`は自動初期化されるらしく、イニシャライザはなくても怒られません。
もちろんあっても良いです
```swift
struct PersonStruct {
    var name: String
}
```

# 違い2(値型と参照型)
### class
```swift
class PersonClass {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}

let personClass1 = PersonClass(name: "めぐみ")
let personClass2 = personClass1
personClass2.name = "たろう" // `personClass2`の`name`を「たろう」に変える

// そうすると、、、
print(personClass1.name) // `personClass1`の`name`も「たろう」に変わる
```

### struct
```swift
struct PersonStruct {
    var name: String
}

var personStruct1 = PersonStruct(name: "めぐみ")
var personStruct2 = personStruct1
personStruct2.name = "たろう" // `personClass2`の`name`を「たろう」に変える

// そうしても、、、
print(personStruct1.name) // `personClass1`の`name`は「めぐみ」のまま
```

# 違い3(継承)
### class
```swift
class PersonClass {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func introduction() {
        print("私は\(name)です")
    }
}

class StudentClass: PersonClass {
    var id: String
    
    init(name: String, id: String) {
        self.id = id
        super.init(name: name) // ここは`PersonClass`のイニシャライザ
    }
    
    override func introduction() {
        print("私は\(name)です。生徒番号は\(id)です。")
    }
}

let student = StudentClass(name: "たけし", id: "123456")
student.introduction() // 私はたけしです。生徒番号は123456です。
```

### struct
できない

# 違い3(可変性)
### class
```swift
class PersonClass {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func rename(newName: String) {
        self.name = newName
    }
}

var personClass = PersonClass(name: "めぐみ")
personClass.rename(newName: "たけし")
print(personClass.name) // たけし
```

### struct
自身のプロパティを変更したいときには、メソッドに`mutating`が必須
```swift
struct PersonStruct {
    var name: String
    
    mutating func rename(newName: String) {
        self.name = newName
    }
}

var personStruct = PersonStruct(name: "めぐみ")
personStruct.rename(newName: "たけし")
print(personStruct.name) // たけし
```

`mutating`ないと怒られる
![スクリーンショット 2023-09-17 20.22.02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/982325a1-55a8-a6f6-959a-6768bed5dd8e.png)


# おわり
ここら辺複雑でむずいです。
理解していないと予期せぬバグを生み出しそうなのでちゃんと勉強します。。。

足りないことや間違ってることがあればコメントで教えてくれると助かります
