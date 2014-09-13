# UIImageView
### how to make circular image and add border?
```objective-c
//circle
self.profileImageView.layer.cornerRadius = self.profileImageView.frame.size.width / 2;
self.profileImageView.clipsToBounds = YES;
//border
self.profileImageView.layer.borderWidth = 3.0f;
self.profileImageView.layer.borderColor = [UIColor whiteColor].CGColor;
```
### how to add clickable action for imageview?
```objective-c
UITapGestureRecognizer *singleTap = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(tapDetected)];
singleTap.numberOfTapsRequired = 1;
self.imageView.userInteractionEnabled = YES;
[self.imageView addGestureRecognizer:singleTap];
```

### long press gesture for image view
[ref](http://stackoverflow.com/questions/17833150/long-press-gesture-and-movement-of-uiimageview)

### for imageview tap gesture, how to reference the sender?
[ref](http://stackoverflow.com/questions/6082244/uitapgesturerecognizer-selector-sender-is-the-gesture-not-the-ui-object)

### how to load images asynchronously from NSURL?
```objective-c
NSURL *imageURL = [NSURL URLWithString:@"http://best-posts.com/wp-content/uploads/2014/07/hottest_world_cup_girls_07.jpg"];
    // download the image asynchronously
    NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:imageURL];
    [NSURLConnection sendAsynchronousRequest:request
                                       queue:[NSOperationQueue mainQueue]
                           completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {
                               if ( !error )
                               {

                                   UIImage *image = [[UIImage alloc] initWithData:data];
                                   [cell.profileImage setImage:image];
                               } else {
                                   NSLog(@"%@", error);
                               }
                           }];
```

### how to cache images?
currently I am using [SDWebImage](https://github.com/rs/SDWebImage)

### iOS how to manually cache an image with sdwebimage?
[reference](http://stackoverflow.com/questions/14902835/sdwebimage-download-image-and-store-to-cache-for-key)

### how to display acitivy indicator when loading image
[reference](http://stackoverflow.com/questions/11262204/show-activity-indicator-in-sdwebimage)
