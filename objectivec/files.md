# Files

### write to *.plist file
```objective-c
- savePlistFile {
    NSString *error;
    NSString *rootPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) objectAtIndex:0];
    NSString *plistPath = [rootPath stringByAppendingPathComponent:@"Data.plist"];
    NSDictionary *plistDict = [NSDictionary dictionaryWithObjects:
            [NSArray arrayWithObjects: personName, phoneNumbers, nil]
            forKeys:[NSArray arrayWithObjects: @"Name", @"Phones", nil]];
    NSData *plistData = [NSPropertyListSerialization dataFromPropertyList:plistDict
                            format:NSPropertyListXMLFormat_v1_0
                            errorDescription:&error];
    if(plistData) {
        [plistData writeToFile:plistPath atomically:YES];
    }
    else {
        NSLog(error);
    }
}
```

### how to delete a *.plist file programmingly
```objective-c
if(![[NSFileManager defaultManager] removeItemAtPath:documentPlistPath error:&error])
    {
        //TODO: Handle/Log error
        NSLog(@"got error");
    }
    else {
        NSLog(@"delete successfuly");
    }
```
### how to copy bundle plist(which is read only) to document plist file(which is writable)?
```objective-c
NSFileManager *fileManager = [NSFileManager defaultManager];
    NSError *error;
    NSArray *documentPaths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsDirectory = [documentPaths objectAtIndex:0];
    NSString *documentPlistPath = [documentsDirectory stringByAppendingPathComponent:@"messages.plist"];
    NSString *bundlePath = [[NSBundle mainBundle] bundlePath];
    NSString *bundlePlistPath = [bundlePath stringByAppendingPathComponent:@"messages.plist"];

    BOOL success = [fileManager copyItemAtPath:bundlePlistPath toPath:documentPlistPath error:&error];
    if (success) {
        NSArray *array = [NSArray arrayWithContentsOfFile:documentPlistPath];
        NSLog(@"success: after copied the plist file is %@", array);
    }
    else {
        NSArray *array = [NSArray arrayWithContentsOfFile:documentPlistPath];
        NSLog(@"fail: after copied the plist file is %@", array);
    }
```

### how to remove file in document path
```objective-c
- (void)removeFile:(NSString *)fileName
{
    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSString *documentsPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) objectAtIndex:0];

    NSString *filePath = [documentsPath stringByAppendingPathComponent:fileName];
    NSError *error;
    BOOL success = [fileManager removeItemAtPath:filePath error:&error];
    if (success) {
        NSLog(@"removed");
    }
    else
    {
        NSLog(@"Could not delete file -:%@ ",[error localizedDescription]);
    }
}
```

