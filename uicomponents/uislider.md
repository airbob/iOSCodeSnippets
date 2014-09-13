#UISlider

### How to add action to UISlider
```objective-c
- (IBAction)sliderValueChanged:(id)sender
{
    // Set the label text to the value of the slider as it changes
    self.label.text = [NSString stringWithFormat:@"%f", self.slider.value];
}
```
