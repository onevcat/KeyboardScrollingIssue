## Demo for a scrolling issue when using collection (scroll) view in custom keyboard view

### What happened?

See [this GIF](https://raw.githubusercontent.com/onevcat/KeyboardScrollingIssue/master/demo.gif).

When using a collection view inside a keyboard view (e.g. by setting `textView.inputView` to your view), the scroll view will get stuck once you tapping a cell while it is scrolling. When it happens, the collection view will not receive any further tapping event, until you do another scrolling to rescue it from that state.

There are several conditions that it could happen:

1. You collection should behave as the view or a subview of a keyboard. Collection views inside a view controller's view works without this issue.
2. Only tapping the last row would cause this issue. Upper rows works well.

It is not a "Delays Contents Touches" or "Cancel content touches" problem. The collection view is using its default setting without any further adjustment. Although I have tried to set the delay touches, nothing would help to solve this issue.

### Reproduce in the Demo

Just build and run. Tap in the text view, and then scroll the "keyboard". When it is still scrolling, tap on any cell in the last row. It should reproduce in both iOS 8 and iOS 9 (and also in simulator, although it is a bit harder to tap the cell quickly enough than in a device).

### How to solve?

Add this method to your collection delegate:

```swift
func scrollViewWillEndDragging(scrollView: UIScrollView, withVelocity velocity: CGPoint, targetContentOffset: UnsafeMutablePointer<CGPoint>) {
        
}
```

You could just leave it empty, and the collection view will work properly in keyboard.

### How do you know it?

By wasting three hours in my life.

### Could you tell me why?

You ask me, I ask who?

OK...it is just a Chinese joke. If you know the reason, would you please leave a note and tell me why? I will be appreciated with any help.