This is a fork of [JakeLin/SwiftWeather](https://github.com/JakeLin/SwiftWeather). Here are the steps I took to get Rollbar integrated into the project *without* cocoapods:

 1. Download the [Rollbar Framework Files](https://github.com/rollbar/rollbar-ios/releases/download/v0.1.5/Rollbar.zip)
 2. Open XCode and Drag the (unzipped) framework files into your solution.
 3. If you don't have a bridging file already correctly working:
    * Add an objective-c (.m) file.
    * XCode will prompt you to create a bridging file, allow it to do so.
    * Open the bridinging file, and add the following lines:
      ```objective-c
       #ifndef ContextJar_Bridging_Header_h

       #define ContextJar_Bridging_Header_h

       #import <SystemConfiguration/SystemConfiguration.h>
       #import <Rollbar/Rollbar.h>

       #endif /* ContextJar_Bridging_Header_h */
       ```
 4. Initialize Rollbar in AppDelegate like so:
    ```swift
    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool     {
        // Override point for customization after application launch.
        let config: RollbarConfiguration = RollbarConfiguration()
        config.environment = "production"

        Rollbar.initWithAccessToken("YOUR ACCESS TOKEN", configuration: config)

        return true
    }
    ```
 5. Now Any Uncaught Objective C style errors will be automatically reported to rollbar
 6. You can use `Rollbar.logWithLevel` to report Swift Style errors manually
