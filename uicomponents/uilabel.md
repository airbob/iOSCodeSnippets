#UILabel


### UILabel auto height implementation
- non auto-layout case
```objective-c
self.mainLabel.lineBreakMode = NSLineBreakByWordWrapping;
self.mainLabel.numberOfLines = 0;
NSString *someText = @"this is a really long long message, this is a really long long message, this is a really long long message, this is a really long long message, this is a really long long message, this is a really long long message, this is a really long long message, this is a really long long message-===== end ";
//key part: calculate the frame size
CGSize maxSize = CGSizeMake(320.f, FLT_MAX);
CGRect labRect = [someText boundingRectWithSize:maxSize options:NSStringDrawingUsesLineFragmentOrigin attributes:@{NSFontAttributeName:self.mainLabel.font} context:nil];
self.mainLabel.frame = CGRectMake(0, 64, maxSize.width, labRect.size.height);
self.mainLabel.text = someText;
```

- auto-layout case
```objective-c
//uilabel inspector: line break mode: word wrap
//add constrains to the UILabel, height >= some value
//If you implement UILabel in UItableView, still use boundingRectWithSize to calculate height of UILabel, then calculate the offset accordingly
```

### Add underline to text in UILabel
```objective-c
NSDictionary *underlineAttribute = @{NSUnderlineStyleAttributeName: @(NSUnderlineStyleSingle)};
myLabel.attributedText = [[NSAttributedString alloc] initWithString:@"Test string" 
                                                         attributes:underlineAttribute];
```
