#UITableView

### Where set table view cell separators:
> tableview-> attribule inspector -> separator -> single line

### Change UITableView separator line color
```objective-c
self.tableView.separatorColor = [UIColor whiteColor];
```

### How to change tableview background color
```
[self.tableView setBackgroundColor:[UIColor yellowColor]];
```

### How to change tableview background image
```
self.tableView.backgroundView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"table_background.png"]];
```

### Customize section head of table view
```
-(UIView *) tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section {
    static NSString *CellIdentifier = @"SectionHeader";
    UITableViewCell *headerView = [tableView dequeueReusableCellWithIdentifier:CellIdentifier];
    if (headerView == nil){
        [NSException raise:@"headerView == nil.." format:@"No cells with matching CellIdentifier loaded from your storyboard"];
    }
    return headerView;
}
```

### height of section head of table view
```
- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section
{
        return 40.0;
}
```

### select tableview cell and goes to another view
```objective-c
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
     [self performSegueWithIdentifier:@"forward" sender:indexPath];
}
```

### How to hide uitableview selection arrow
```
cell.accessoryType = UITableViewCellAccessoryNone;
```
### how to change tableview cell alpha value:
```objective-c
cell.contentView.alpha = 0.5;
```
### how to add different separator for dif tableview cells
```objective-c
//in viewdidload add:
self.tableView.separatorColor = [UIColor clearColor];
//in cellForRowAtIndexPath add
CALayer *separator = [CALayer layer];
        separator.backgroundColor = [UIColor whiteColor].CGColor;
        separator.frame = CGRectMake(0, -1, self.view.frame.size.width, 1);
        [cell.layer addSublayer:separator];
```
### particular cell is not selectable
```objective-c
    if (indexPath.row == 0)
    {
        // we decide here that first cell in the table is not selectable (it's just an indicator)
        cell.selectionStyle = UITableViewCellSelectionStyleNone;
    }
```
### select tableview cell and perform segue with some parameters:
```objective-c
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
	[self performSegueWithIdentifier:@"editEvent" sender:[self.tableView cellForRowAtIndexPath:indexPath]];
}
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
{
    UITableViewCell *cell = sender;
    // Make sure your segue name in storyboard is the same as this line
    NSLog(@"inside prepare for segue");
    if ([[segue identifier] isEqualToString:@"editEvent"])
    {
        //((BTCSegue *)segue).animationType = 0 ;
        // Get reference to the destination view controller
        llEditLogViewController *editViewController = [segue destinationViewController];
        NSIndexPath *indexPath = [self.tableView indexPathForCell:cell];
        NSInteger rowSelected = [indexPath row];
        editViewController.rowSelected = rowSelected;
        NSLog(@"prepare for segue, and row is %ld",(long)rowSelected);
    }
}

### how to rename delete table view cell "Delete"?
```objective-c
//let's say we want to rename it to close
- (NSString *)tableView:(UITableView *)tableView titleForDeleteConfirmationButtonForRowAtIndexPath:(NSIndexPath *)indexPath {
    return @"Close";
}
```

### Delete the extra separator of UITableView in iOS 7
```objective-c
- (UIView *)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section
{
    return [UIView new];
    // If you are not using ARC:
    // return [[UIView new] autorelease];
}
```

### long press to re-ordering tableview cells
[reference](https://github.com/bvogelzang/BVReorderTableView)

### how to implement movable/reorder tableview cells?
[ref1](https://github.com/yonat/EditableList)

### problem: swipe to delete tableview cell seems not working any more.
https://github.com/John-Lluch/SWRevealViewController/issues/104

### swipe to delete table view cell?
```objective-c
- (BOOL)tableView:(UITableView *)tableView canEditRowAtIndexPath:(NSIndexPath *)indexPath
{
    // Return YES - we will be able to delete all rows
    return YES;
}

- (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath
{
    // Perform the real delete action here. Note: you may need to check editing style
    //   if you do not perform delete only.
    NSLog(@"Deleted row.");
}
```

### how to change UITableViewCellAccessory-DisclosureIndicator colour
```objective-c
//normally replace the arrow with an image

cell.accessoryView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"disclosureIndicator.png"]];
```
### how to add search bar in tableview
[reference](http://www.appcoda.com/search-bar-tutorial-ios7/)

### UISearchResultsTableView dequeueReusableCellWithIdentifier error?
```objectiv-c
// use self.tableview insead of tableview when dequeue with identifier
```

### how to reload data in tableview of a container view?
```objective-c
UITableViewController *tbc = (UITableViewController *)self.childViewControllers[0];
[tbc.tableView reloadData];
```

### how to make tableview Header not show captalized letter?

```objective-c
- (void)tableView:(UITableView *)tableView willDisplayHeaderView:(UIView *)view forSection:(NSInteger)section
{
    if([view isKindOfClass:[UITableViewHeaderFooterView class]]){
        UITableViewHeaderFooterView *tableViewHeaderFooterView = (UITableViewHeaderFooterView *) view;

        NSString *tempStr = [tableViewHeaderFooterView.textLabel.text lowercaseString];
        tempStr = [tempStr stringByReplacingCharactersInRange:NSMakeRange(0,1) withString:[[tempStr substringToIndex:1] uppercaseString]];
        NSLog(@"temp Str is %@", tempStr);
        tableViewHeaderFooterView.textLabel.text = tempStr;
    }
}
```

### how to add load more function at bottom of tableview?
1. define a cell identifier as the bottom loading bar
```objective-c
-(void) tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath
{
    int lastRow=[tableArray count];
    if([indexPath row] == lastRow)
    {
        NSLog(@"going to load more");//implement your load more function
        [self.tableView reloadData];
        [self.tableView setNeedsDisplay];
        }
}
```
### tableview cell can not select
common reasons: <br>
1. do you have tap gesture in the view controller? <br>
2. did you write did selection method correctly? <br>
### how to set uitableviewcell selection style
```objective-c
cell.selectionStyle = UITableViewCellSelectionStyleNone;
```

### table view refresh and empty view message?
http://www.appcoda.com/pull-to-refresh-uitableview-empty/

### tableview auto height
http://www.raywenderlich.com/73602/dynamic-table-view-cell-height-auto-layout
