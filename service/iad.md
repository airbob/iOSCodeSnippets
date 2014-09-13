# iAd

### how to add iAd:
case 1: juse add a normal iAd banner at bottom of view:
step 1: build phase add linked framework (iAds) <br/>
step 2: add ```#import <iAd/iAd.h>``` in *.h file, in *.m viewdidLoad add ``` self.canDisplayBannerAds = YES;```<br>
[Reference](http://www.youtube.com/watch?v=fP2ijcXbCz4)
[Reference2](http://stackoverflow.com/questions/19717446/how-to-have-an-in-app-purchase-to-remove-iads)

case 2: add iAd banner in the view
step1: add framework <br>
step2: import iAd and add ADBannerViewDelegate <br>
step3: add banner to view, drag and link IBOutlet<br>
step4: add following methods:

```objective-c
-(void)bannerView:(ADBannerView *)banner
didFailToReceiveAdWithError:(NSError *)error{
    NSLog(@"Error in Loading Banner!");
}

-(void)bannerViewDidLoadAd:(ADBannerView *)banner{
    NSLog(@"iAd banner Loaded Successfully!");
}
-(void)bannerViewWillLoadAd:(ADBannerView *)banner{
    NSLog(@"iAd Banner will load!");
}
-(void)bannerViewActionDidFinish:(ADBannerView *)banner{
    NSLog(@"iAd Banner did finish");

}
```

