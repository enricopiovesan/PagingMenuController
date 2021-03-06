![](https://raw.githubusercontent.com/wiki/kitasuke/PagingMenuController/images/logo.png)

[![CI Status](http://img.shields.io/travis/kitasuke/PagingMenuController.svg?style=flat)](https://travis-ci.org/kitasuke/PagingMenuController)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/kitasuke/PagingMenuController)
[![Version](https://img.shields.io/cocoapods/v/PagingMenuController.svg?style=flat)](http://cocoapods.org/pods/PagingMenuController)
[![License](https://img.shields.io/cocoapods/l/PagingMenuController.svg?style=flat)](http://cocoapods.org/pods/PagingMenuController)
[![Platform](https://img.shields.io/cocoapods/p/PagingMenuController.svg?style=flat)](http://cocoapods.org/pods/PagingMenuController)

This library is inspired by [PageMenu](https://github.com/uacaps/PageMenu)

## Updates

See [CHANGELOG](https://github.com/kitasuke/PagingMenuController/blob/master/CHANGELOG.md) for details

*** Swift 2.0 ***  
Please use swift_2.0 branch if you want to try in Swift 2.0

## Description

### Flexible menu width mode

<img src="https://raw.githubusercontent.com/wiki/kitasuke/PagingMenuController/images/demo4.gif" width="160" height="284">

### Fixed menu width mode

<img src="https://raw.githubusercontent.com/wiki/kitasuke/PagingMenuController/images/demo2.gif" width="284" height="160">

### Segmented control mode

<img src="https://raw.githubusercontent.com/wiki/kitasuke/PagingMenuController/images/demo3.gif" width="160" height="284">

## Customization

* default page index to show as a first view
```Swift
defaultPage: Int
```
* background color for menu view
```Swift
backgroundColor: UIColor
```
* background color for selected menu item
```Swift
selectedBackgroundColor: UIColor
```
* text color for menu item
```Swift
textColor: UIColor
```
* text color for selected menu item
```Swift
selectedTextColor: UIColor
```
* font for menu item text
```Swift
font: UIFont
```
* menu position
```Swift
menuPosition: MenuPosition
```
* height for menu view
```Swift
menuHeight: CGFloat
```
* margin for each menu item
```Swift
menuItemMargin: CGFloat
```
* duration for menu item view animation
```Swift
animationDuration: NSTimeInterval
```
* menu display mode and scrolling mode
```Swift
menuDisplayMode: MenuDisplayMode

public enum MenuDisplayMode {
  case FlexibleItemWidth(centerItem: Bool, scrollingMode: MenuScrollingMode)
  case FixedItemWidth(width: CGFloat, centerItem: Bool, scrollingMode: MenuScrollingMode)
  case SegmentedControl
}

public enum MenuScrollingMode {
  case ScrollEnabled
  case ScrollEnabledAndBouces
  case PagingEnabled
}
```
if `centerItem` is true, selected menu item is always on center
  
if `MenuScrollingMode` is `ScrollEnabled` or `ScrollEnabledAndBouces`, menu view allows scrolling to select any menu item
if `MenuScrollingMode` is `PagingEnabled`, menu item should be selected one by one 

* menu item mode
```Swift
public var menuItemMode = MenuItemMode.Underline(height: 3, color: UIColor.whiteColor(), selectedColor: UIColor.blueColor())
public enum MenuItemMode {
    case None
    case Underline(height: CGFloat, color: UIColor, selectedColor: UIColor)
    case RoundRect(radius: CGFloat, horizontalScale: CGFloat, verticalScale: CGFloat, selectedColor: UIColor)
}
```

## Usage

`import PagingMenuController` to use PagingMenuController in your file.

### Using Storyboard

```Swift
let viewController = self.storyboard?.instantiateViewControllerWithIdentifier("ViewController") as! ViewController
viewController.title = "Menu title"
let viewControllers = [viewController]

let pagingMenuController = self.childViewControllers.first as! PagingMenuController

let options = PagingMenuOptions()
options.menuHeight = 60
options.menuDisplayMode = PagingMenuOptions.MenuDisplayMode.FlexibleItemWidth(centerItem: true, scrollingMode: PagingMenuOptions.MenuScrollingMode.PagingEnabled)
pagingMenuController.setup(viewControllers: viewControllers, options: options)
```
* You should add `ContainerView` into your view controller's view and set `PagingMenuController` as the embedded view controller's class

### Coding only
```Swift
let viewController = UIViewController()
viewController.title = "Menu title"
let viewControllers = [viewController]

let options = PagingMenuOptions()
options.menuItemMargin = 5
options.menuDisplayMode = PagingMenuOptions.MenuDisplayMode.SegmentedControl
let pagingMenuController = PagingMenuController(viewControllers: viewControllers, options: options)

self.addChildViewController(pagingMenuController)
self.view.addSubview(pagingMenuController.view)
pagingMenuController.didMoveToParentViewController(self)
```

### Delegate methods (optional)

```Swift
pagingMenuController.delegate = self
```

```Swift
func willMoveToMenuPage(page: Int) {
}

func didMoveToMenuPage(page: Int) {
}
```

## Requirements

iOS8 or later  
Swift 1.2 or later  
Xcode 6.3 or later  

## Installation

### CocoaPods
PagingMenuController is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '8.0'
use_frameworks!

pod "PagingMenuController"
```

Then, run `pod install`

In case you haven't installed CocoaPods yet, run the following command

```ruby
$ gem install cocoapods
```

### Carthage
PagingMenuController is available through [Carthage](https://github.com/Carthage/Carthage).

To install PagingMenuController into your Xcode project using Carthage, specify it in your Cartfile:

```ruby
github "kitasuke/PagingMenuController"
```

Then, run `carthage update`

You can see `Carthage/Build/iOS/PagingMenuController.framework` now, so drag and drop it to `Linked Frameworks and Libraries` in General menu tab with your project.
Add the following script to `New Run Script Phase` in Build Phases menu tab.
```ruby
/usr/local/bin/carthage copy-frameworks
```

Also add the following script in `Input Files`
```ruby
$(SRCROOT)/Carthage/Build/iOS/PagingMenuController.framework
```

In case you haven't installed Carthage yet, run the following command

```ruby
$ brew update
$ brew install carthage
```

### Manual

Copy all the files in `Pod/Classes` directory into your project.

## License

PagingMenuController is available under the MIT license. See the [LICENSE](https://github.com/kitasuke/PagingMenuController/blob/master/LICENSE) file for more info.
