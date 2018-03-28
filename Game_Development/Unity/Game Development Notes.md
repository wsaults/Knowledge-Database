# Game Development

### 3D Modeling

- [Maya LT](http://www.autodesk.com/products/maya-lt/overview) - Maya is the industry leading 3D modeling package. Recently, Maya LT was released, which is a version specifically for game development.
- [Blender](https://www.blender.org/) - Blender is a free and open source 3D modeling package with features that are comparable to paid modeling programs.
- [zBrush](http://pixologic.com/) - zBrush is relatively new compared to other 3D modeling applications, and it offers a very unique workflow that many artists prefer over traditional techniques.

### Texturing

- [Substance Designer & Substance Painter](https://www.allegorithmic.com/) - Substance Designer and Substance Painter from Allegorithmic are quickly becoming the gold standard in texturing software because of their modern toolsets and workflows.
- [Quixel](http://quixel.se/) - The Quixel Suite is a robust set of add-ons for Photoshop that cater to artists that already have well-established texturing workflows in Photoshop.
- [GameTextures.com](http://gametextures.com/) - GameTextures.com is a fantastic library of pre-made textures that can be applied directly or remixed for use in a game.



## Setup the project

####Change the following settings to help with frame rate if these are not needed.

Open: Window > Lighting > Settings

- Uncheck Realtime Global Illuminatic


- Uncheck Baked Global Illumination
- Uncheck Auto Generate



Open: Edit > Project Settings > Player

Here you can change how your game is deployed to various platforms.

Other Settings:

- Color Space: Linear



Open: Edit > Project Settings > Quality

Keep the Fastest and Fantastic settings.

Change "Fastest" to "Low Quality" and change "Texture Quality" to "Quarter Res"



## Main Camera

1 unit of transform in unity is roughly equal to 1 meter in the real world.

Clipping Planes: Near & Far. - The distance that the camera will render object.

Image Effect: Change the way the camera renders the scene. Such as a filter.

Free image effects are available on the asset store under "post procesing stack".