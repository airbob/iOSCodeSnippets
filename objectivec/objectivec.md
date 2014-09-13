#Objecitve-C

### + and - in objective-c
- ```+``` class method
- ```-``` instance method

### filename1+filename2.h/m
> That is the convention for naming files, that contain categories for existing classes. Categories are a way of adding methods to an existing class in Objective-C, without subclassing

### method to convert hex color to UIColor
```objective-c
-(UIColor *)colorFromHex:(NSString *)hex {
    unsigned int c;
    if ([hex characterAtIndex:0] == '#') {
        [[NSScanner scannerWithString:[hex substringFromIndex:1]] scanHexInt:&c];
    } else {
        [[NSScanner scannerWithString:hex] scanHexInt:&c];
    }
    return [UIColor colorWithRed:((c & 0xff0000) >> 16)/255.0
                           green:((c & 0xff00) >> 8)/255.0
                            blue:(c & 0xff)/255.0 alpha:1.0];
}
```

### use notification to update view of another view controller
```objecitve-c
//code here
```

### call a method for every 60 seconds

```objecitve-c
- (void)viewDidLoad
{
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
    [NSTimer scheduledTimerWithTimeInterval:60.0
                                     target:self
                                   selector:@selector(someMethod)
                                   userInfo:nil
                                    repeats:YES];
}

- (void) someMethod {
    NSLog(@"hello I am called");
}
```
### how to parse json data without knowing theire keys?
```objecitve-c
    NSString *prefix=@"http://ec2-54-251-248-32.ap-southeast-1.compute.amazonaws.com/backup/db/samquery1.php?userid=";
    NSInteger uid = 100;     //let's say user id is 111
    NSString *postfix = [NSString stringWithFormat:@"%ld", (long)uid];
    NSString *qstring = [ prefix stringByAppendingString:postfix];
    NSURL *url=[NSURL URLWithString:qstring];
    NSData *data=[NSData dataWithContentsOfURL:url];

    NSError *error=nil;
    NSArray *jsonArray =[NSJSONSerialization JSONObjectWithData:data options:
                         NSJSONReadingMutableContainers error:&error];
    if (!jsonArray) {
        NSLog(@"Error parsing JSON: %@", error);
    } else {
        for(NSDictionary *item in jsonArray) {
            //NSLog(@"Item: %@", item);
            //NSString *negemo = [item objectForKey:@"negemo"];
            //NSLog(@"negative emo is %@", negemo);

            NSLog(@"=====start of row=====\n");
            NSArray *keys = [item allKeys];
            for (id key in keys)
            {
                id aValue = [item objectForKey:key];
                NSLog(@"key is %@ and value is %@",key,aValue);
            }
            NSLog(@"=====end of row=====\n");
        }
    }
```

### how to implement iOS7 back swipe gesture?
[reference](http://stackoverflow.com/questions/23321332/how-to-create-custom-back-swipe-gesture-in-uinavigationcontroller-on-ios-7)


### NSArray and NSMutableArray
```objective-c
NSArray* arr = [[NSArray alloc]initWithObjects:@"work",@"email",@"dreamon",@"aaa",@"bbb",@"ccc", nil];
NSMutableArray *randomSelection =  [[NSMutableArray alloc]init];
[randomSelection addObject:@"string1"];
```
### NSString and NSMutableString 区别?
```objective-c
//NSString is immutable , it equals to constant NSMutableString
//NSMutableString is mutable

```

### how to generate months array?

```objective-c
NSArray *monthlySymbols = [[[NSDateFormatter alloc] init] shortMonthSymbols];
```

### how to iterate date from one year ago to today?
```objective-c
    NSDate *now = [NSDate date];
    NSDate *seventyDaysAgo = [now dateByAddingTimeInterval:-356*24*60*60];
    //NSLog(@"70 days ago: %@", seventyDaysAgo);

    NSDateFormatter *dateFormatter = [[NSDateFormatter alloc] init];
	[dateFormatter setDateFormat:@"yyyy-MM-dd"];
	//NSString *MyString = [dateFormatter stringFromDate:seventyDaysAgo];



    NSCalendar *calendar = [NSCalendar currentCalendar];
    NSDateComponents *oneDay = [[NSDateComponents alloc] init];
    [oneDay setDay: 1];

    for (NSDate* date = seventyDaysAgo; [date compare: now] <= 0;
         date = [calendar dateByAddingComponents: oneDay
                                          toDate: date
                                         options: 0] ) {
             //NSLog( @"%@ in [%@,%@]", date, sevenDaysAgo, now );
             NSLog(@"date is %@", [dateFormatter stringFromDate:date]);
         }
```

### how to use blocks?

[ref1](http://rypress.com/tutorials/objective-c/blocks.html)
[ref2](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/ProgrammingWithObjectiveC.pdf)
[ref3](http://stackoverflow.com/questions/19171206/save-a-completion-handler-as-an-object)

### remind the user after some period did not open the app
[reference](http://www.youtube.com/watch?v=fnhIVCz2xJ4)
### NSDate how to get several days ago?
```objective-c
NSDate *now = [NSDate date];
NSDate *sevenDaysAgo = [now dateByAddingTimeInterval:-7*24*60*60];
NSLog(@"7 days ago: %@", sevenDaysAgo);
```

### weak/strong/assign/copy/retain discussion
[reference](http://stackoverflow.com/questions/8927727/objective-c-arc-strong-vs-retain-and-weak-vs-assign(

### use applescript to auto login itunes
[reference](http://computers.tutsplus.com/tutorials/creating-an-applescript-to-switch-between-multiple-itunes-accounts--mac-49681)


### iOS with different URL:
[reference](http://iosdevelopertips.com/cocoa/launching-other-apps-within-an-iphone-application.html)

### where to check Mac error code
[ref](http://www.opensource.apple.com/source/CarbonHeaders/CarbonHeaders-18.1/MacErrors.h)


### what is the best way to detect device landscape or not?
```objective-c
- (BOOL)isLandscape
{
    UIInterfaceOrientation orientation = [UIApplication sharedApplication].statusBarOrientation;
    if(orientation == 0 || orientation == UIInterfaceOrientationPortrait)
        return NO;
    else
        return YES;

    //return UIDeviceOrientationIsLandscape([UIDevice currentDevice].orientation); //this is not accurate some times
}
```

### @class forward declaration
http://stackoverflow.com/questions/3904663/what-does-class-do-in-objective-c

