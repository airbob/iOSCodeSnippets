#UINavigationController

### Go to previous view in navigation controoler
```objective-c
[self.navigationController popViewControllerAnimated:TRUE];
```

### when add segue for modal view -> navigation controller view, the navigation bar disappears.
Please connect segue from modal view to navigation controller, not the navigation controller root view

