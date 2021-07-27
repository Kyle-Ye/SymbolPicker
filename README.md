# Symbol Picker

A SF Symbols picker for Mac apps. Built with AppKit.

## Usage

![screenshot of Symbol Picker](https://raw.githubusercontent.com/francisfeng/SymbolPicker/main/images/screenshot.PNG)

1. AppKit
```swift

// in your NSViewController subclass
import SymbolPicker

@objc func pickIcon(_ sender: NSMenuItem) {
  if let windowController = SymbolPicker.windowController(
      symbol: collection.symbol,
      color: collection.color ?? .labelColor,
      delegate: self,
      title: collection.name),
     let iconSheet = windowController.window {
    
    // You need to persist this windowController in your app.
    symbolPickerWindowController = windowController
    
    window.beginSheet(iconSheet) {
      _ in
      self.symbolPickerWindowController = nil
    }
  }
}

extension ViewController: SymbolPickerDelegate {
  func symbolPicker(_ symbol: String, color: NSColor?) {
  
  }
}
```

2. SwiftUI

I haven't try it with SwiftUI yet. Any contributions will be welcome.

## Known Issues

1. The UI is a little laggy compared with the SF Symbols app from Apple.

2. Memory footprint will go up everytime the window is presented and dimissed. Too much work has went into it and I think it's now acceptable after a few symbol selections. Any contributions will be welcome.

3. The app can't be presented like a modal dialog. I don't know why. Any help will be appreciated. To mimic the experience, the window is not movable or resizable. You may also want to implement `Escape` to dismiss dialog in your app. You can do this by overriding   `func mouseDown(with: NSEvent)` in your `NSWindowController` subclass.

```swift
override func mouseDown(with event: NSEvent) {
  super.mouseDown(with: event)
  if let sheetwindow = window?.attachedSheet {
    window?.endSheet(sheetwindow)
  }
}
```

## Lisense
MIT
