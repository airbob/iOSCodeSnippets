#Network

### How to implement asynchronous calls

```objecitve-c
//define a background queue at beginning of file
#define mainBgQueue dispatch_get_global_queue( DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)
//issue the async calls
dispatch_async(mainBgQueue, ^{
        NSData* data = [NSData dataWithContentsOfURL: yourURL];
        //then continue deal with the data
        [self performSelectorOnMainThread:@selector(manipulateData:)
               withObject:data waitUntilDone:YES];
    });
- (void)manipulateData:(NSData *)responseData {
//your method here
}
```

### synchronous GET
```objective-c
NSURL *url = [NSURL URLWithString:@"https://blockchain.info/tobtc?currency=USD&value=1"];
NSString *webData= [NSString stringWithContentsOfURL:url];
NSLog(@"%@",webData);
```
