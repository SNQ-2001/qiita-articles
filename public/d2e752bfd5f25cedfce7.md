---
title: 【SwiftUI】iOS16からのタグレイアウト
tags:
  - iOS
  - Swift
  - SwiftUI
private: false
updated_at: '2023-06-16T00:22:11+09:00'
id: d2e752bfd5f25cedfce7
organization_url_name: avis-inc
slide: false
ignorePublish: false
---
# はじめに
タグのレイアウトを実装したくて、ネットで検索してもいい感じの実装ができるコードが見つからず、自分で実装するか〜と思ってたらAppleのドキュメントにタグレイアウトの完璧なコードがあったので記事にしておきます。

# デザイン
|右寄せ|中央寄せ|左寄せ|
|-|-|-|
|![Simulator Screenshot - iPhone 14 Pro - 2023-06-15 at 22.41.54.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/f101dbba-b8aa-03f9-cc3a-c569b4b4d6aa.png)|![Simulator Screenshot - iPhone 14 Pro - 2023-06-15 at 22.41.38.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/61d6dc6d-5d71-6a95-d1cc-36609a7cc5d3.png)|![Simulator Screenshot - iPhone 14 Pro - 2023-06-16 at 00.19.06.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1745371/204a28b1-f4ab-9dfc-30f1-1653b76f0b15.png)|

# 実装
```swift
import SwiftUI

struct FlowLayout: Layout {
    var alignment: Alignment = .center
    var spacing: CGFloat?

    func sizeThatFits(proposal: ProposedViewSize, subviews: Subviews, cache: inout Void) -> CGSize {
        let result = FlowResult(
            in: proposal.replacingUnspecifiedDimensions().width,
            subviews: subviews,
            alignment: alignment,
            spacing: spacing
        )
        return result.bounds
    }

    func placeSubviews(in bounds: CGRect, proposal: ProposedViewSize, subviews: Subviews, cache: inout Void) {
        let result = FlowResult(
            in: proposal.replacingUnspecifiedDimensions().width,
            subviews: subviews,
            alignment: alignment,
            spacing: spacing
        )
        for row in result.rows {
            let rowXOffset = (bounds.width - row.frame.width) * alignment.horizontal.percent
            for index in row.range {
                let xPos = rowXOffset + row.frame.minX + row.xOffsets[index - row.range.lowerBound] + bounds.minX
                let rowYAlignment = (row.frame.height - subviews[index].sizeThatFits(.unspecified).height) *
                alignment.vertical.percent
                let yPos = row.frame.minY + rowYAlignment + bounds.minY
                subviews[index].place(at: CGPoint(x: xPos, y: yPos), anchor: .topLeading, proposal: .unspecified)
            }
        }
    }

    struct FlowResult {
        var bounds = CGSize.zero
        var rows = [Row]()

        struct Row {
            var range: Range<Int>
            var xOffsets: [Double]
            var frame: CGRect
        }

        init(in maxPossibleWidth: Double, subviews: Subviews, alignment: Alignment, spacing: CGFloat?) {
            var itemsInRow = 0
            var remainingWidth = maxPossibleWidth.isFinite ? maxPossibleWidth : .greatestFiniteMagnitude
            var rowMinY = 0.0
            var rowHeight = 0.0
            var xOffsets: [Double] = []
            for (index, subview) in zip(subviews.indices, subviews) {
                let idealSize = subview.sizeThatFits(.unspecified)
                if index != 0 && widthInRow(index: index, idealWidth: idealSize.width) > remainingWidth {
                    finalizeRow(index: max(index - 1, 0), idealSize: idealSize)
                }
                addToRow(index: index, idealSize: idealSize)

                if index == subviews.count - 1 {
                    finalizeRow(index: index, idealSize: idealSize)
                }
            }

            func spacingBefore(index: Int) -> Double {
                guard itemsInRow > 0 else { return 0 }
                return spacing ?? subviews[index - 1].spacing.distance(to: subviews[index].spacing, along: .horizontal)
            }

            func widthInRow(index: Int, idealWidth: Double) -> Double {
                idealWidth + spacingBefore(index: index)
            }

            func addToRow(index: Int, idealSize: CGSize) {
                let width = widthInRow(index: index, idealWidth: idealSize.width)

                xOffsets.append(maxPossibleWidth - remainingWidth + spacingBefore(index: index))
                remainingWidth -= width
                rowHeight = max(rowHeight, idealSize.height)
                itemsInRow += 1
            }

            func finalizeRow(index: Int, idealSize: CGSize) {
                let rowWidth = maxPossibleWidth - remainingWidth
                rows.append(
                    Row(
                        range: index - max(itemsInRow - 1, 0) ..< index + 1,
                        xOffsets: xOffsets,
                        frame: CGRect(x: 0, y: rowMinY, width: rowWidth, height: rowHeight)
                    )
                )
                bounds.width = max(bounds.width, rowWidth)
                let ySpacing = spacing ?? ViewSpacing().distance(to: ViewSpacing(), along: .vertical)
                bounds.height += rowHeight + (rows.count > 1 ? ySpacing : 0)
                rowMinY += rowHeight + ySpacing
                itemsInRow = 0
                rowHeight = 0
                xOffsets.removeAll()
                remainingWidth = maxPossibleWidth
            }
        }
    }
}

private extension HorizontalAlignment {
    var percent: Double {
        switch self {
        case .leading: return 0
        case .trailing: return 1
        default: return 0.5
        }
    }
}

private extension VerticalAlignment {
    var percent: Double {
        switch self {
        case .top: return 0
        case .bottom: return 1
        default: return 0.5
        }
    }
}
```

# 使い方
```swift
import SwiftUI

struct ContentView: View {
    private let tags = ["Swift", "iOS開発", "SwiftUI", "UIKit", "WWDC", "Python", "JavaScript", "PHP", "Ruby", "Flutter", "Dart", "Android", "iPhone"]
    var body: some View {
        FlowLayout(alignment: .center, spacing: 7) {
            ForEach(tags, id: \.self) { tag in
                Text(tag)
                    .padding(.vertical, 5)
                    .padding(.horizontal, 12)
                    .background(Color(.systemGroupedBackground))
                    .cornerRadius(15)
            }
        }
        .padding(20)
    }
}
```

# ドキュメント
https://developer.apple.com/documentation/swiftui/food_truck_building_a_swiftui_multiplatform_app/

# おわり
Appleのドキュメントにくっついてるサンプルプロジェクトの充実具合やばいです。
めっちゃ勉強になります。
