---
title: 【SwiftUI】Realmを使ってみた
tags:
  - iOS
  - Swift
  - Realm
  - RealmSwift
  - SwiftUI
private: false
updated_at: '2023-04-15T21:55:53+09:00'
id: c7dfa9e9e65ebc4334be
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
普段、ローカルデータベースを使うときはCoreDataを使うのですが、Realmを使う機会があったので記録しておきます。

https://github.com/realm/realm-swift

# 実装
```swift:RealmEntity
import Foundation
import RealmSwift

public class RealmEntity: Object {
    @Persisted(primaryKey: true) public var id: Int = 0
}
```

```swift:RealmRepository
import Foundation
import RealmSwift

public protocol RealmRepositoryProtocol {
    func get() -> Results<RealmEntity>
    func add(_ bookmark: RealmEntity) throws
    func delete(_ bookmark: RealmEntity) throws
}

public final class RealmRepository: RealmRepositoryProtocol {
    let realm: Realm
    
    public init(realm: Realm = try! Realm()) {
        self.realm = realm
    }
    
    public func get() -> Results<RealmEntity> {
        realm.objects(RealmEntity.self)
    }
    
    public func add(_ bookmark: RealmEntity) throws {
        try realm.write {
            realm.add(bookmark)
        }
    }
    
    public func delete(_ bookmark: RealmEntity) throws {
        guard let bookmark = realm.object(ofType: RealmEntity.self, forPrimaryKey: bookmark.id) else {
            throw NSError(domain: "primary key not found", code: 0)
        }
        try realm.write {
            realm.delete(bookmark)
        }
    }
}
```

```swift:ContentView
import SwiftUI

struct ContentView: View {
    private let repository = RealmRepository()
    var body: some View {
        VStack(spacing: 50) {
            Button {
                print(Array(repository.get()))
            } label: {
                Text("取得")
            }
            
            Button {
                let realmEntity = RealmEntity()
                realmEntity.id = 0
                try? repository.add(realmEntity)
            } label: {
                Text("保存")
            }
            
            Button {
                let realmEntity = RealmEntity()
                realmEntity.id = 0
                try? repository.delete(realmEntity)
            } label: {
                Text("削除")
            }
        }
    }
}
```

# おわり
CoreDataより数倍簡単でした。
今度からRealmを使おうと思います。
