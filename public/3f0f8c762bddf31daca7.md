---
title: 【Swift】Alamofireでasync/awaitを使う
tags:
  - iOS
  - async
  - Swift
  - Alamofire
  - await
private: false
updated_at: '2022-10-18T13:09:11+09:00'
id: 3f0f8c762bddf31daca7
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
「alamofire async」で検索すると`withCheckedThrowingContinuation`を使ってasyncを使用している記事が多く出てきますが、実は標準でasync/awaitを使えるみたいです。
今回はそのやり方を紹介できたらと思います。

# やりかた
### String
```swift
let response = await AF.request(url, method: .get, headers: headers).serializingString().response
switch response.result {
case .success(let data):
    print(type(of: data)) // String
case .failure(let error):
    print(type(of: error)) // AFError
}
```

### Data
```swift
let response = await AF.request(url, method: .get, headers: headers).serializingData().response
switch response.result {
case .success(let data):
    print(type(of: data)) // Data
case .failure(let error):
    print(type(of: error)) // AFError
}
```

### Decodable
```swift
let response = await AF.request(url, method: .get, headers: headers).serializingDecodable(StatusesShow.self).response
switch response.result {
case .success(let data):
    print(type(of: data)) // StatusesShow
case .failure(let error):
    print(type(of: error)) // AFError
}
```

### カスタムレスポンス
カスタムレスポンスの作成方法は[こちら](https://qiita.com/SNQ-2001/items/4771cf3a91f6470bbc14)
```swift
let result = await AF.request(url, method: .get, headers: headers).serializingResponse(using: TwitterDecodableResponseSerializer<StatusesShow>()).value
switch result {
case .success(let data):
    print(type(of: data)) // StatusesShow
case .failure(let error):
    print(type(of: error)) // TwitterError
}
```

# おわり
日本語の記事が1つも見つからなかったので意外と知られてないかも？？

https://github.com/Alamofire/Alamofire/releases/tag/5.5.0
