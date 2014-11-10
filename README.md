xcode6-iboutlet-crash-case
==========================

Xcode6 is crash on debugging time with project mixing Swift and ObjC and using IBOutlet.

This repository is uploaded on [github](https://github.com/omochi/xcode6-iboutlet-crash-case)

# How to reproduce

1. Clone with `$ git clone` this repository.
2. Open xcodeproj by `Xcode 6.1(6A1052d)`
3. Put breakpoint on ViewController/viewDidLoad (Line 16).
4. Run on iOS device.
5. Xcode.app will crash.

# Occuring conditions

According to my investigation, occuring conditions are below.

- Swift project.
- Custom view class is link to IBOutlet property.
- Custom view class is written by ObjC.
- Custom view class header is `#import`ed by other header which is `#import`ed by Swift-ObjC-Briding header.
- Both import statements set force above are not using double quote `"FooLib.h"` but angle bracket `<FooLib/FooLib.h>`.
- In Xcode build setting, `Header search paths` is not using `$SRCROOT/` but `./` .

# My easy workaround

Last condition is easy to avoid by changing relative path to absolute with `$SRCROOT`
