# UIWebView

### how to add activityIndicator during webview loading?
```objective-c
- (void)viewDidLoad
{
    [super viewDidLoad];
    NSString * urlString = @"......";
    [_postWebView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:urlString]]];
    _postWebView.delegate = self;
}

- (void)webViewDidStartLoad:(UIWebView *)webView{
    [self.postProgress setHidden:NO];
    [self.postProgress startAnimating];

}

- (void)webViewDidFinishLoad:(UIWebView *)webView{
    [self.postProgress stopAnimating];
    [self.postProgress setHidden:YES];
}
```

### get URL source code:
```objective-c
NSURL *mobileurl = [NSURL URLWithString:@"http://campusbus.ntu.edu.sg/ntubus/index.php/m/main"];
    NSError* error = nil;
    NSString* text = [NSString stringWithContentsOfURL:mobileurl encoding:NSASCIIStringEncoding error:&error];
    if( text )
    {
        NSLog(@"Text=%@", text);
    }
    else
    {
        NSLog(@"Error = %@", error);
    }
```
### how to disable uiwebview(content editable html) cursor auto move (very slightly)?
this is because "automatic bring-field-into-view scrolling when you navigate around a web form" <br>
For my case, I added listener to keyboard show and hide, during keyboard will show/hide set uiwebview.scrollview bounds to webview.bounds <br>

```objective-c
- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    if (self.duringWillKeyboard)
        scrollView.bounds = self.webView.bounds;
```
[reference](https://stackoverflow.com/questions/15926260/set-uiwebview-content-not-to-move-when-keyboard-is-shown)

### in uiwebview.scrollview scroll, some of html body style(such as height:100%) not refreshed, how to dynamically change body height?
after some debugging I found ```webview.frame``` and ```webview.scrollview.frame``` wont change, the only thing change is ```webview.scrollview.contentoffset.y```

so execute javascript code after scrolling:
```objective-c
- (void)stoppedScrolling
{
    float newHeight = _htmlBodyHeight + self.webView.scrollView.contentOffset.y;
    NSLog(@"old height is %f, new height is %f", _htmlBodyHeight, newHeight);
    NSString *jsCode = [NSString stringWithFormat:@"document.body.style.height = '%fpx'",newHeight];// @"document.body.style.height = '1000px'";
    [self.webView stringByEvaluatingJavaScriptFromString:jsCode];
}
```
[REF](http://stackoverflow.com/questions/993280/how-to-detect-when-a-uiscrollview-has-finished-scrolling)

### how to remove extra view in keyboard when using UIWebview has input field?
[ref1](http://stackoverflow.com/questions/8470984/how-to-remove-prev-next-button-from-virtual-keyboard-ios)
[ref2](https://gist.github.com/bjhomer/2048571)

### how to load local html
```
NSURL *url = [[NSBundle mainBundle] URLForResource:@"index" withExtension:@"html"];
    NSURLRequest* request = [NSURLRequest requestWithURL:url];
    [webView loadRequest:request];
```

### how to auto scroll uiwebview when typing ?
[ref](http://stackoverflow.com/questions/8523232/automatic-scrolling-when-contenteditable-designmode-in-a-uiwebview)
[ref2](http://stackoverflow.com/questions/13867411/i-am-using-content-editable-html-loaded-in-uiwebview-i-need-the-code-to-set-the)

### How to debug UIWebView with browser(say safari)
- Add ```[NSClassFromString(@"WebView") performSelector:@selector(_enableRemoteInspector)];``` to appDelegate didFinishLaunchingWithOptions
- In safari preference->advanced to show develop in menu
- safari -> develop select the device/simulator and click on the webpage loaded to debug


