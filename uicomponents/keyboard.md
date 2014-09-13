#KeyBoard

### how to dismiss keyboard when taps non-editable area on the screen
- method1

```objective-c
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    for (UIView * txt in self.view.subviews){
        if ([txt isKindOfClass:[UITextField class]] && [txt isFirstResponder]) {
            [txt resignFirstResponder];
        }
    }
}
```
- method 2

```objective-c
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    [self.view endEditing:YES];
}
```

- method 3
```objective-c
### dismiss decimal pad:
 UITapGestureRecognizer *tapRecgonizer = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(tap:)];
    [self.view addGestureRecognizer:tapRecgonizer];
- (void) tap: (UIGestureRecognizer* ) gr
{
    NSLog(@"YES, YOU JUST TAPPED");
    [self.view endEditing:YES];
}
```

### How to set keyboard return action?
```objective-c
//1: add UITextFieldDelegate and set delegate to the view controller
//2: implement textFieldShouldReturn method
- (BOOL)textFieldShouldReturn:(UITextField *)textField {
    [textField resignFirstResponder];
    return YES;
}
```

### how to move view up when keyboard shows up
1. add listener to keyboard show or hide<br>
2. set the center (up keyboard height: 216px) when keyboard shows <br>
3. reset to original center after keyboard hide <br>
[reference](http://stackoverflow.com/questions/16752154/move-uiview-when-keyboard-appears)
[reference](http://stackoverflow.com/questions/15036519/scroll-uitextfield-above-keyboard-in-a-uitableviewcell-on-a-regular-uiviewcontro)

### keyboard display same animation as other views?
[ref](http://stackoverflow.com/questions/19709749/animate-uiview-along-keyboard-appear-animation)



