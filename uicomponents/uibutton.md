#UIButton

### add ```UIButton``` dynamically and associated them with ```IBAction``` 
```objecitve-c
UIButton *myButton = [[UIButton alloc] init...];
[myButton addTarget:something action:@selector(myAction) forControlEvents:UIControlEventTouchUpInside];
```

### how to access ```UIButton``` in ```UITableViewCell```
- method1: without subclass of UITableViewCell
```objective-c
//first need to set tag to UIButton
//then reference it by its tag as below
UIButton *button2 = (UIButton *)[[cell contentView] viewWithTag:2];
```
- method2: with subclass of UITableViewCell
```objective-c
//add connection of UIButton to IBOutlets in UITableViewCell
//then easily reference the button via
cell.myButton
```

### How to add link to button click?

```objective-c
-(void) buttonpressed:(UIButton *)sender 
{
    NSString* launchUrl = @"http://apple.com/";
    [[UIApplication sharedApplication] openURL:[NSURL URLWithString: launchUrl]];
}
```

### How to set ```UIButton``` round corner
```objective-c
self.button.layer.masksToBounds = YES;
self.button.layer.cornerRadius = 5.0;
```

### How to add colored border to ```UIButton```
```objective-c
[[self.button layer] setBorderWidth:2.0f];
[[self.button layer] setBorderColor:[UIColor whiteColor].CGColor];
```

