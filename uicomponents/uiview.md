# UIView

### how to add line to UIView?
```objective-c
UIView * separator = [[UIView alloc] initWithFrame:CGRectMake(20, 104, 320, (1.0 / [UIScreen mainScreen].scale) / 2)];
    separator.backgroundColor = [UIColor colorWithWhite:0.7 alpha:1];
    [self.view addSubview:separator];
```
#### how to make the line exactly 1px for both normal iOS device as well as retina display device?
```objective-c
CGFloat scaleOfMainScreen = [UIScreen mainScreen].scale;
    CGFloat alwaysOnePixelInPointUnits = 1.0/scaleOfMainScreen;

    UIView * separator = [[UIView alloc] initWithFrame:CGRectMake(20, 40, 300, alwaysOnePixelInPointUnits)];
    separator.backgroundColor = [UIColor colorWithWhite:1 alpha:0.2];
    [self.view addSubview:separator];
```
### dismiss keyboard when user taps other area:
```objective-c
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    for (UIView * txt in self.view.subviews){
        if ([txt isKindOfClass:[UITextField class]] && [txt isFirstResponder]) {
            [txt resignFirstResponder];
        }
    }
}

/*OR*/

- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    [self.view endEditing:YES];
}
```

[reference](http://stackoverflow.com/questions/18756196/how-to-dismiss-keyboard-when-user-tap-other-area-outside-textfield)


### how to set view background image?

```objective-c
self.view.backgroundColor = [UIColor colorWithPatternImage:[UIImage imageNamed:@"randomgrey.png"]];
```

#### how to stretch the image if size not fit?
```objective-c
    UIGraphicsBeginImageContext(self.view.frame.size);
    [[UIImage imageNamed:@"chat_blur_default9"] drawInRect:self.view.bounds];
    UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    self.view.backgroundColor = [UIColor colorWithPatternImage:image];
```

### how to add uiview programmingly ?
```objective-c
UIView *cv = [[UIView alloc]initWithFrame:CGRectMake(0, self.view.frame.size.height, 320, 216)]; //creat an instance of your custom view
    cv.backgroundColor = [UIColor colorWithRed:0.941 green:0.941 blue:0.941 alpha:1];
    [self.view addSubview:cv]; // add to your main view
```

