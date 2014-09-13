#UINavigationBar


### How to add action to UINavigation title?
- method 1: add ```UIButton``` to it
- method 2: add tap gesture to it
[reference](http://stackoverflow.com/questions/2077025/uinavigationbar-touch)

### How to set navigation bar title with a text field?
```objective-c
UITextField *textField = [[UITextField alloc]initWithFrame:CGRectMake(0, 0, 200, 22)];
textField.text = @"Insert Title Here";
textField.font = [UIFont boldSystemFontOfSize:19];
textField.textColor = [UIColor whiteColor];
textField.textAlignment = NSTextAlignmentCenter;
textField.delegate = self;
self.navigationItem.titleView = textField;
```

### To show/hide navigation bar
```objective-c
//hide Navigation bar :
[self.navigationController setNavigationBarHidden:YES animated:YES];
//show Navigation bar :
[self.navigationController setNavigationBarHidden:NO animated:YES];
```
### how to change navigation bar tint color

```objective-c
self.navigationController.navigationBar.barTintColor = [UIColor colorWithRed:26/255.0f green:188/255.0f blue:156/255.0f alpha:1.0f];
self.navigationController.navigationBar.tintColor = [UIColor whiteColor];
[self.navigationController.navigationBar setTitleTextAttributes:@{NSForegroundColorAttributeName : [UIColor whiteColor]}];
self.navigationController.navigationBar.translucent = NO;
```
### how remove the 1px black border under navigation bar?
```
//need to add a subview to overlay it
UIView *navBorder = [[UIView alloc] initWithFrame:CGRectMake(0,navigationBar.frame.size.height-1,navigationBar.frame.size.width, 1)];

// Change the frame size to suit yours //

[navBorder setBackgroundColor:[UIColor colorWithWhite:200.0f/255.f alpha:0.8f]];
[navBorder setOpaque:YES];
[navigationBar addSubview:navBorder];
[navBorder release];
```
more discussion can be found [here](http://stackoverflow.com/questions/19226965/how-to-hide-ios7-uinavigationbar-1px-bottom-line)

