# iOS: Quick Look at Face Tracking

> This talk covers: AR Face Tracking using the TrueDepth camera.

> Great tutorial and main source of information for this talk: [raywenderlich.com/ios-facetracking](https://www.raywenderlich.com/5491-ar-face-tracking-tutorial-for-ios-getting-started)

## Vocabulary:

- **TrueDepth:** Front faceing camera available on the iPhone X and later which uses an IR emiiter to send out 30,000 dots. The IR camera then interprets those dots.
- **ARKit:** Apple iOS framework for producing augmented reality experiences on your device.
- **ARSCNView:** A view for displaying AR experiences that augment the camera view with 3D SceneKit content.
- **SceneKit:** Apple iOS framework for rendering 3D content.
- **SCNNode:** Represents a position and transform in a 3D space. It has no visible content but you can attach geometry, lights, cameras and other things.
- **ARSession:** Does crazy things like read data from the device's motion sensing hardware and performing image analysis on captured images.
- **ARFaceTrackingConfiguration:** A configuration that tracks the movement and expressions of the user's face with the TrueDepth camera.
- **ARAnchor:** Positions in the real world tracked by ARKit, which do not move when you move your phone.
- **ARFaceAnchor:** Extends ARAnchor and includes information about a face, such as topology and expression.
- **ARFaceGeometry:** 3D description of a face including verticies and textureCoordinates.
- **ARSCNFaceGeometry:** Essentially creates what you see on the screen composed of SCNGeometry which uses data from an ARFaceGeometry.
- **SCNGeometry:** 3D shape aka model or mesh that can be displayed in a scene with materials that define its appearance.

## Let's get started!

1. Import `ARKit` into your view controller.
  ```
  import ARKit
  ```

2. Change your view controller class to `ARSCNView` inside the storyboard.

> Note: `ARSCNView` is for displaying augmented reality experiences using `SceneKit` content. It can show the camera feed and display `SCNNode`s.

3. Create an `IBOutlet` for your view.

4. 