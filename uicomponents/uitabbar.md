#UITabBar

### How to change tab bar sytles (color,set image)
```objective-c
//in app delegate  didFinishLaunchingWithOptions add lines such as
[[UITabBar appearance] setTintColor:[UIColor whiteColor]];
[[UITabBar appearance] setBarTintColor:[UIColor yellowColor]];
[[UITabBar appearance] setSelectedImageTintColor:[UIColor greenColor]];
//tab bar image unselected color
[[UIView appearanceWhenContainedIn:[UITabBar class], nil] setTintColor:[UIColor whiteColor]];
//for the unselect image color, it can only work once, how to solve it
UITabBarItem *item0 = [self.tabBar.items objectAtIndex:0];
item0.image = [[UIImage imageNamed:@"tab1Unselect.png"] imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
item0.selectedImage = [UIImage imageNamed:@"tab1Select.png"];
```


### how to hide tab bar if needed:
```objective-c
self.tabBarController.tabBar.hidden=YES;
```

### how to get position of each tab bar?
```
for (UIView* view in self.tabBar.subviews)
    {
        NSLog(@"view descritipon %@", view.description);
    }
```

### tab bar click how to go to first view of navigation controller
```objective-c
- (void)tabBarController:(UITabBarController *)tabBarController didSelectViewController:(UIViewController *)viewController {
  if (viewController != tabBarItemForNavControllerTab) {
    [self.navControllerInFirstTab popToRootViewControllerAnimated:NO];
  }
}
```


