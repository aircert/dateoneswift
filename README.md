Date One Challenge App
===============================

The Date One Challenge App app is a very simple application meant to get a new developer
started using the OpenTok iOS SDK.

Quick Start
-----------

To use this application:

1.  Install CocoaPods as described in [CocoaPods Getting Started](https://guides.cocoapods.org/using/getting-started.html#getting-started).
 
2. In Terminal, `cd` to your project directory and type `pod install`.
 
3. Reopen your project in Xcode using the new `.xcworkspace` file.

4. When you run the application, it connects to an OpenTok session and
   publishes an audio-video stream from your device to the session.

5. Run the app on a second client. You can do this by deploying the app to an
   iOS device and testing it in the simulator at the same time. 

   When the second client connects, it also publishes a stream to the session,
   and both clients subscribe to (view) each other’s stream.

Application Notes
-----------------

*   Follow the code from the `ViewController.viewDidLoad(_:)` method through
    to the OpenTok callbacks to see how streams are created and handled in
    the OpenTok iOS SDK.

*   By default, all delegate methods from classes in the OpenTok iOS SDK are
    invoked on the main queue. This means that you can directly modify the view
    hierarchy from inside the callback, without any asynchronous callouts.

*   When the main view loads, the ViewController calls the
    `OTSession.initWithApiKey(_:, sessionId:,delegate:)` method to initialize
    a Session object. The app then calls the
    `OTSession.connectWithToken(_:, error:)` to connect to the session. The
    `OTSessionDelegate.sessionDidConnect(_:)` message is sent when the app
    connects to the OpenTok session.

*   The `doPublish()` method of the app initializes a publisher and passes it
    into the `OTSession.publish(_:,error:)` method. This publishes an
    audio-video stream to the session.

*   The `OTSessionDelegate.session(_:,streamCreated:)` message is sent when
    a new stream is created in the session. In response, the
    method calls `OTSubscriber(stream:,delegate:)`,
    passing in the OTStream object. This causes the app to subscribe to the
    stream.

 To add a second publisher (which will display as a subscriber in your emulator), either run the app a second time in an iOS device or use the OpenTok Playground to connect to the session in a supported web browser (Chrome, Firefox, or Internet Explorer 10-11) by following the steps below:


Configuration Notes
-------------------

*   You can test in the iOS Simulator or on a supported iOS device. However, the
    XCode iOS Simulator does not provide access to the camera. When running in
    the iOS Simulator, an OTPublisher object uses a demo video instead of the
    camera.

[1]: https://tokbox.com/account/#/
[2]: https://tokbox.com/developer/sdks/server/
