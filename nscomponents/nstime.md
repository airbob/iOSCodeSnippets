# NSTime

### how to parse standard time string and format it (eg: 2014-01-02 10:10:10)?
```objective-c
formatter.dateFormat = @"yyyy-MM-dd HH:mm:ss";
formatter.timeZone = [NSTimeZone timeZoneWithAbbreviation:@"UTC"];
NSDate *date = [formatter dateFromString:[tmpDict objectForKey:@"posttime"]];
NSDateFormatter *formatter2 = [[NSDateFormatter alloc] init];
formatter2.dateFormat = @"dd-MMM HH:mm";
NSString *postTime = [formatter2 stringFromDate:date];
NSLog(@" post time is %@", postTime);
```

