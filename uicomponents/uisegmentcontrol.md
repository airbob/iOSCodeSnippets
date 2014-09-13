#UISegmentControl

### How to add IBAction to UISegmentControl
```objective-c
- (IBAction)searchSegmentedControl:(UISegmentedControl *)sender
{
    switch (sender.selectedSegmentIndex) {
        case 0:
            NSLog(@"First was selected");
            break;
        case 1:
            NSLog(@"Second was selected");
            break;
        case 2:
            NSLog(@"Third was selected");
            break;
        default:
            break;
    }
}
```
