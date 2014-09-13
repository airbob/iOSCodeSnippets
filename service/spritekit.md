# SpriteKit
### how to add a node with image name

```objective-c
CGPoint location = [touch locationInNode:self];

        SKSpriteNode *sprite = [SKSpriteNode spriteNodeWithImageNamed:@"Spaceship"];

        sprite.position = location;

        SKAction *action = [SKAction rotateByAngle:M_PI duration:1];

        [sprite runAction:[SKAction repeatActionForever:action]];

        [self addChild:sprite];

```
### how to detect general SKNode touched?
```objective-c
-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    UITouch *touch = [touches anyObject];
    CGPoint touchLocation = [touch locationInNode:self];
    SKNode *touchedNode = [self nodeAtPoint:touchLocation];

    NSLog(@"touchLocation x: %f and y: %f", touchLocation.x, touchLocation.y);

    if (touchedNode != self) {
        NSLog(@"Removed from parent.");
        //[touchedNode removeFromParent];
        UIViewController *vc = self.view.window.rootViewController;
        [vc performSegueWithIdentifier:@"toSettings" sender:nil];
    }
}

```

### how to detect certain SKNode touched?

```objective-c
//assign the name property when add the node:
        //      second label
        SKLabelNode *myLabel2 = [SKLabelNode labelNodeWithFontNamed:@"Chalkduster"];
        //        myLabel2.userInteractionEnabled = YES;
        myLabel2.name = @"nodename";
        myLabel2.text = @"Hello, World!";
        myLabel2.fontSize = 30;
        myLabel2.position = CGPointMake(100, 100);
        [self addChild:myLabel2];

-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {
    UITouch *touch = [touches anyObject];
    CGPoint touchLocation = [touch locationInNode:self];
    SKNode *touchedNode = [self nodeAtPoint:touchLocation];

    NSLog(@"touchLocation x: %f and y: %f", touchLocation.x, touchLocation.y);

    if ([touchedNode.name isEqualToString:@"nodename"]) {
        NSLog(@"Removed from parent.");
        //[touchedNode removeFromParent];
        UIViewController *vc = self.view.window.rootViewController;
        [vc performSegueWithIdentifier:@"toSettings" sender:nil];
    }
}
```

## game center:
step1: add GameKit framework<br>
step2: import ```#import <GameKit/GameKit.h>``` and add ```GKGameCenterControllerDelegate```
step3: add authenticate function:
```objective-c
#pragma mark - game center functions
[self authenticateLocalPlayer];
-(void)authenticateLocalPlayer{
    GKLocalPlayer *localPlayer = [GKLocalPlayer localPlayer];

    localPlayer.authenticateHandler = ^(UIViewController *viewController, NSError *error){
        if (viewController != nil) {
            [self presentViewController:viewController animated:YES completion:nil];
        }
        else{
            if ([GKLocalPlayer localPlayer].authenticated) {
                _gameCenterEnabled = YES;

                // Get the default leaderboard identifier.
                [[GKLocalPlayer localPlayer] loadDefaultLeaderboardIdentifierWithCompletionHandler:^(NSString *leaderboardIdentifier, NSError *error) {

                    if (error != nil) {
                        NSLog(@"%@", [error localizedDescription]);
                    }
                    else{
                        _leaderboardIdentifier = leaderboardIdentifier;
                        NSLog(@"leader board identifier name is %@", _leaderboardIdentifier);
                    }
                }];
            }

            else{
                _gameCenterEnabled = NO;
            }
        }
    };
}
```
### how to integrate game center in your app?
[Ref1](http://www.appcoda.com/ios-game-kit-framework/)
[Ref2](http://www.raywenderlich.com/3276/game-center-tutorial-for-ios-how-to-make-a-simple-multiplayer-game-part-12)


