#Debug

### How to take screenshot in simulator
- method1: edit->copy screen -> open preview ->paste
- method2: cmd + s

### How to change simulator size
> cmd + 1/2/3

### AdHoc distribution
[reference](http://help.apple.com/iosdeployment-apps/mac/1.1/#app43ad871e)

### change project name in Xcode, but its name just does not change
Please search for whole project of CFBundleDisplayName, maybe it is hardcoded somewhere.

### how to get iPhone simulator directory?
```
dirPaths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    docsDir = dirPaths[0];
    NSLog(@"%@",docsDir);
```

### how to view sqlite visually on mac?
[try this](https://itunes.apple.com/us/app/sqlite-professional-read-only/id635299994?mt=12)

### how to use instruments?
[reference](http://www.raywenderlich.com/23037/how-to-use-instruments-in-xcode)
