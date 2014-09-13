#NSUserDefaults

### how to set and get NSUserDefaults
```objective-c
//when set
[[NSUserDefaults standardUserDefaults] setObject:textField.text forKey:@"mainTitle"];
[[NSUserDefaults standardUserDefaults] synchronize];
//when get
NSString *tempTitle = [[NSUserDefaults standardUserDefaults] objectForKey:@"mainTitle"];
```
