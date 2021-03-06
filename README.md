# DIYCam

DIYCam is a high-level layer built on top of AVFoundation that enables simple setup and implementation of photo and video capture within iOS. It is pretty darn opinionated though... if you are looking for lots of configuration options then this is probably not the best way to go. If you are looking for something simple but hopefully not "too" simple then read on:

## Getting Started
The fastest way to get started with DIYCam is to look through the included "Example" project, but the setup and use is designed to be really minimal.
```objective-c
// Init camera
cam = [[DIYCam alloc] init];
[[self cam] setDelegate:self];
[[self cam] setup];

// Preview
cam.preview.frame       = display.frame;
[display.layer addSublayer:cam.preview];

CGRect bounds           = display.layer.bounds;
cam.preview.bounds      = bounds;
cam.preview.position    = CGPointMake(CGRectGetMidX(bounds), CGRectGetMidY(bounds));
```

## Required Frameworks
    AssetsLibrary.framework
    AVFoundation.framework
    CoreGraphics.framework
    CoreMedia.framework
    MobileCoreServices.framework
    QuartzCore.framework
    
## Configuration
Default configuration settings can be modified within DIYCamDefaults.h where options for asset library use, orientation, device settings, and quality can be modified.

## Methods
```objective-c
- (void)setup;
- (void)startPhotoCapture;
- (void)startVideoCapture;
- (void)stopVideoCapture;
- (NSString *)createAssetFilePath:(NSString *)extension;
```

## Delegate Methods
```objective-c
- (void)camReady:(DIYCam *)cam;
- (void)camDidFail:(DIYCam *)cam withError:(NSError *)error;
- (void)camCaptureStarted:(DIYCam *)cam;
- (void)camCaptureStopped:(DIYCam *)cam;
- (void)camCaptureProcessing:(DIYCam *)cam;
- (void)camCaptureComplete:(DIYCam *)cam withAsset:(NSDictionary *)asset;
```

## Properties
```objective-c
@property (nonatomic, assign) id <DIYCamDelegate> delegate;
@property (nonatomic, retain) AVCaptureSession *session;
@property (nonatomic, assign) AVCaptureVideoPreviewLayer *preview;
@property (nonatomic, assign) BOOL isRecording;
```