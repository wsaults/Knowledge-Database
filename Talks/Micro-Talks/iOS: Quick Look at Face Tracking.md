# iOS: Quick Look at Face Tracking

> This talk covers: AR Face Tracking using the TrueDepth camera.

> Great tutorial and main source of information for this talk: [raywenderlich.com/ios-facetracking](https://www.raywenderlich.com/5491-ar-face-tracking-tutorial-for-ios-getting-started)


## Vocabulary:

- **TrueDepth:** Front-facing camera available on the iPhone X and later which uses an IR emiiter to send out 30,000 dots. The IR camera then interprets those dots.
- **ARKit:** Apple iOS framework for producing augmented reality experiences on your device.
- **ARSCNView:** A view for displaying AR experiences that augment the camera view with 3D SceneKit content.
- **SceneKit:** Apple iOS framework for rendering 3D content.
- **SCNNode:** Represents a position and transform in a 3D space. It has no visible content but you can attach geometry, lights, cameras and other things.
- **ARSession:** Does crazy things like read data from the device's motion sensing hardware and performing image analysis on captured images.
- **ARFaceTrackingConfiguration:** A configuration that tracks the movement and expressions of the user's face with the TrueDepth camera.
- **ARAnchor:** Positions in the real world tracked by ARKit, which do not move when you move your phone.
- **ARFaceAnchor:** Extends ARAnchor and includes information about a face, such as topology and expression.
- **ARFaceGeometry:** 3D description of a face including verticies and textureCoordinates. It has 1220 verticies. #9 being the nose.
- **ARSCNFaceGeometry:** Essentially creates what you see on the screen composed of SCNGeometry which uses data from an ARFaceGeometry.
- **SCNGeometry:** 3D shape aka model or mesh that can be displayed in a scene with materials that define its appearance.
- **Blend Shape Coefficients:** There are currently 52 blend shape coefficients that rand grom 0.0 (no expression) to 1.0 (maximum expression)

## Let's get started!

Intro
  - How/why I learned about this
  - Ask for a Volunteer

1. **Nothing:** Talk about `TrueDepth` camera
  - iPhone X front-facing camera.
  - Unlock phone, Animojis 

2. **Mesh:** Talk about `ARKit`, `SceneKit`, `ARFaceGeometry`.
  - IR emits/tracks 30,000 dots to create a mesh mask
  - Things are rendered using `SceneKit`
  - Geometry consists of verticies and textureCoordinates

  > A vertex is a corner.

3. **Nose:** Talk about `ARAnchor`, `SCNNode`.
  - Anchor: Real world positions that don't move with the phone.
  - `anchor.geometry.verticies` #9 is the nose. (1220)
  - Node: position with no content that can have things attached to it.

  > Tap to change the nose!

4. **Face:** Talk about `ARFaceAnchor`, Blend Shape Coefficients (52)
  - FaceAnchor: topology and expression "the geometry of the face"
  - BSC: describes how much expression your face is showing. 0.0 to 1.0 (min to max)

  ```
  let features = ["nose", "leftEye", "rightEye", "mouth"]
  let featureIndices = [[9], [1064], [42], [24, 25]]
  ```



### Whiteboard notes:
- Vertex is a corner
- 30,000 IR dots
- 1220 verticies
- 52 BSC's 0.0 to 1.0
- Animoji
- FaceAnchor
- Node
- Smilies
- IR and Anchors and Nodes, oh my!