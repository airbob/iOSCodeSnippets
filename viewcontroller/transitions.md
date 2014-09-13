# Transitions

### how to implement the normal "swipe left for settings side bar" ?
[reference](http://www.appcoda.com/ios-programming-sidebar-navigation-menu/)

### simple drop down list
[ref](http://www.edumobile.org/iphone/iphone-programming-tutorials/a-simple-drop-down-list-for-iphone/)

### left/right swipe segue
```objective-c
//in view did load//
{
    UISwipeGestureRecognizer *rightRecognizer = [[UISwipeGestureRecognizer alloc] initWithTarget:self action:@selector(rightSwipeHandle:)];
    rightRecognizer.direction = UISwipeGestureRecognizerDirectionRight;
    [rightRecognizer setNumberOfTouchesRequired:1];
    [self.view addGestureRecognizer:rightRecognizer];
    UISwipeGestureRecognizer *leftRecognizer = [[UISwipeGestureRecognizer alloc] initWithTarget:self action:@selector(leftSwipeHandle:)];
    leftRecognizer.direction = UISwipeGestureRecognizerDirectionLeft;
    [leftRecognizer setNumberOfTouchesRequired:1];
    [self.view addGestureRecognizer:leftRecognizer];
    }

    - (void)rightSwipeHandle:(UISwipeGestureRecognizer*)gestureRecognizer
{
    [self.navigationController popViewControllerAnimated:YES];
}

- (void)leftSwipeHandle:(UISwipeGestureRecognizer*)gestureRecognizer
{
    [self performSegueWithIdentifier:@"forward" sender:self];
}
```

### how to add app walkthrough?
1. detect whether the user is first time launching app or not [Reference](http://stackoverflow.com/a/13335636/874585)
2. perform segue to walkthrough view if it is first time user [Refenrence](http://www.appcoda.com/uipageviewcontroller-storyboard-tutorial/)

### how to add side bar to the view
[reference](http://www.appcoda.com/ios-programming-sidebar-navigation-menu/)



### how to implement a dropdown list
[example1](https://github.com/nmattisson/DropdownMenu)
[example2](https://github.com/romaonthego/REMenu)
[example3](https://github.com/BijeshNair/NIDropDown)


### how to add iOS default share sheet?
```objective-c

    NSString *text = @"hello world";
            NSURL *url = [NSURL URLWithString:@"http://airbob.github.io/lifeNumber"];
            //UIImage *image = [UIImage imageNamed:@"roadfire-icon-square-200"];

            UIActivityViewController *controller =
            [[UIActivityViewController alloc]
             initWithActivityItems:@[text, url]
             applicationActivities:nil];


            controller.excludedActivityTypes = @[UIActivityTypePrint,
                                                 UIActivityTypeCopyToPasteboard,
                                                 UIActivityTypeAssignToContact,
                                                 UIActivityTypeSaveToCameraRoll,
                                                 UIActivityTypeAddToReadingList,
                                                 UIActivityTypeAirDrop];
            [self presentViewController:controller animated:YES completion:nil];
```

### how to dismiss view controller after certain animation (such as modal view, partial curl)
```objective-c
[self dismissViewControllerAnimated:YES completion:nil];
```
### how to display and dismiss modal view programmingly?
```objective-c
[self presentViewController:modalViewController animated:YES completion:nil];
[self dismissViewControllerAnimated:YES completion:nil];
```


### when display a modal view programmingly, it displays a balck screen, why?
```objective-c
CBModalViewController* modalViewController = [[CBModalViewController alloc] init];
/*this is inconrect if you use storyboard, use following method
(please note the controller identifier is the storyboard id in storyboard
*/

    UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                             bundle: nil];

    CBModalViewController * modalViewController = (CBModalViewController*)[mainStoryboard
    instantiateViewControllerWithIdentifier: @"CBModalViewController"];
```

### how to set starting view controller conditionally?
1. uncheck is initial view in storyboard
2.
```objective-c
self.window = [[UIWindow alloc] initWithFrame:UIScreen.mainScreen.bounds];
    UIStoryboard *storyboard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
    CBFBViewController * startViewController = (CBFBViewController*)[storyboard instantiateViewControllerWithIdentifier: @"CBFBViewController"];

    self.window.rootViewController = startViewController;
    [self.window makeKeyAndVisible];
```
[reference](http://stackoverflow.com/questions/10428629/programatically-set-the-initial-view-controller-using-storyboards)


### whose view is not in the window hierarchy problem
normally add the present controller in viewdidappear instead of viewdidload

### how to implement default iOS7 setting back swipe gesture?
[reference](http://stackoverflow.com/questions/17209468/how-to-disable-back-swipe-gesture-in-uinavigationcontroller-on-ios-7)
```objective-c
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];

    // Disable iOS 7 back gesture
    if ([self.navigationController respondsToSelector:@selector(interactivePopGestureRecognizer)]) {
        self.navigationController.interactivePopGestureRecognizer.enabled = YES;
        self.navigationController.interactivePopGestureRecognizer.delegate = self;
    }
}

- (BOOL)gestureRecognizerShouldBegin:(UIGestureRecognizer *)gestureRecognizer
{
    return YES;
}
```


