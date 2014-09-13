#UIAlertView

### How to add textfield to UIAlertView
```objective-c
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Title"
                                                message:@"Message"
                                               delegate:self
                                      cancelButtonTitle:@"Done"
                                      otherButtonTitles:nil];
alert.alertViewStyle = UIAlertViewStylePlainTextInput;
[alert show];


-(void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex{
    NSLog(@"%@", [alertView textFieldAtIndex:0].text);
}
```

### dismiss alertview after 5 seconds if user did not click on OK
```objective-c
//method1
[self performSelector:@selector(hideAlertView:) withObject:staticalertView afterDelay:5]
//method2
dispatch_async(dispatch_get_main_queue(), ^{
        [self performSelector:@selector(hideAlertView:) withObject:staticalertView afterDelay:5];
    });
```
