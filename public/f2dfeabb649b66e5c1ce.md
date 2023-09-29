---
title: 特定の時間のみ指定可能なTimePickerを作る
tags:
  - Swift
  - SwiftUI
private: false
updated_at: '2021-10-15T23:01:36+09:00'
id: f2dfeabb649b66e5c1ce
organization_url_name: null
slide: false
ignorePublish: false
---
完成形はこんな感じです
![ezgif.com-gif-maker.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/a8ed537c-6bef-6c3c-c110-a51b6d1b9fb0.gif)

今回は00と30のみ指定可能なTimePickerを作成します
minuteIntervalを指定する事で選択を制限することができますがUXが悪いのでこっちがおすすめです
説明することもないのでコードのみ載せておきます

#UIKit
```
class ViewController: UIViewController {
    let timePicker: UIDatePicker = {
        let dp = UIDatePicker()
        dp.datePickerMode = UIDatePicker.Mode.time
        dp.timeZone = NSTimeZone.local
        dp.preferredDatePickerStyle = .wheels
        dp.locale = Locale.init(identifier: "Japanese")
        dp.addTarget(self, action: #selector(timeChange), for: .valueChanged)
        return dp
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        timeChange()
        
        timePicker.backgroundColor = .white
        timePicker.tintColor = UIColor.black
        timePicker.translatesAutoresizingMaskIntoConstraints = false
        self.view.addSubview(timePicker)
        timePicker.clipsToBounds = true
        timePicker.layer.cornerRadius = 10.0
    }
    
    @objc func timeChange() {
        let minutes = DateFormatter()
        minutes.timeZone = .current
        minutes.timeStyle = .short
        minutes.dateStyle = .none
        minutes.locale = NSLocale.system
        minutes.dateFormat = "m"
        
        let SelectTime = Calendar.current.date(byAdding: .hour, value: -3, to: timePicker.date)!
        let Minutes = Int(minutes.string(from: SelectTime))!
        if 0 < Minutes && Minutes < 30 {
            let modifiedDate = Calendar.current.date(byAdding: .minute, value: 30 - Minutes, to: timePicker.date)!
            timePicker.date = modifiedDate
        }
        if 30 < Minutes && Minutes < 60 {
            let modifiedDate = Calendar.current.date(byAdding: .minute, value: 60 - Minutes, to: timePicker.date)!
            timePicker.date = modifiedDate
        }
    }
}
```

#SwiftUI
```
struct ContentView: View {
    @State private var TIME = Date()
    var body: some View {
        VStack {
            DatePicker("", selection: $TIME, displayedComponents: .hourAndMinute)
                .frame(width: 300, height: 60)
                .datePickerStyle(WheelDatePickerStyle())
                .labelsHidden()
                .cornerRadius(10)
                .onChange(of: TIME) { i in
                    ChangeTime()
                }
        }
        .onAppear() {
            ChangeTime()
        }
    }
    func timeM() -> String {
        let dateFormatter = DateFormatter()
        dateFormatter.timeZone = .current
        dateFormatter.timeStyle = .short
        dateFormatter.dateStyle = .none
        dateFormatter.locale = NSLocale.system
        dateFormatter.dateFormat = "m"
        let mString = dateFormatter.string(from: TIME)
        return mString
    }
    func ChangeTime() {
        let mString = timeM()
        let m = Int(mString)!
        if 0 < m && m < 30 {
            let NextTime = Calendar.current.date(byAdding: .minute, value: 30 - m, to: TIME)!
            TIME = NextTime
            print(TIME)
        } else {
            if 30 < m && m < 60 {
                let NextTime = Calendar.current.date(byAdding: .minute, value: 60 - m, to: TIME)!
                TIME = NextTime
                print(TIME)
            }
        }
    }
}
```

UIKitは全然理解してないのでおかしい部分があるかもです
思った通りに動いてるので良しとしてください笑
