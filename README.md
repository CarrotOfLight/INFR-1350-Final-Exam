# INFR 1350 Final Exam

This used textures found on google images



This use a pack man model found:

Retro Pac-Man (Super Smash Bros. Ultimate) - Download Free 3D model by peteandf (@peteandf) \[7496389]





Hologram Texture



I decided to add the hologram texture above the game scene to give the game some sort of retro feel to it by adding those TV static lines (I don’t know the term for them). The hologram shader was added by first creating the different properties for the material, the most important being transparency, line speed and line frequency. To implement these I had to use an in curve to indicate where the lies would be. This was done by first obtaining the y values of uv in world space, multiplying them by frequency and then adding the rate at which they would travel on the axis. After this the lines were given a sharp appearance by using step to make them all one solid color.

The second part of it was using alpha blending to add transparency to the entire object so we would be able to see through it.

To achieve the desired effect I had it set to a high line speed and frequency to make the gaps between lines small. This also gave the game a retrogration effect since the line moved slightly slower to the way the waves moved.



\#Scrolling Texture (waterscrolling)



I decided that the addition of a Scrolling texture to the sides of the screen would be a good way to make packman feel like it's in an arcade setting. What this means is that I wanted the game to catch your attention the moment you looked at it. The fast moving textures do this very well. The way this texture works is by finding the uv’s in world space and having them scroll over time continuously over a fixed rate of time. This is done by first finding the uv coordinates of both textures in the vertex shader and transforming it into clip space to pass along to the fragment shader. The fragment shader then scrolls the textures over a fixed rate of time. These are then blended 50/50 to obtain the final pixel color. I decided to add a speed function to them so I could change the rate at which they were moving. This was done by adding a range for speed and then multiplying the time with the speed in the fragment shader.





\#LUT Color Correction + bumpmap/normal map + rimlight)



I decided to use LUT color correction to enhance the scene's bumpmap and make the rimlight of the Power food (the thing that lets you eat ghosts) more visible and also affect the surrounding bumpmap. This was done to create a more retro feel to the game but also adding textures to it making it seem more realistic and to make the important objects able to stand out more when interacting with the bumpmap.



LUT Color Correction Color correction is used to manipulate the camera's perception of saturation and hue to alter the displayed image to achieve the desired appearance. I used it in this scene to make everything appear overall darker like a dungeon in retro games. To do this in the scene i followed these steps: Use an image editor to achieve the desired color (normal LUT also works very well) Add shader Add material (add shader to this) Add lut to material Create canvas image > scale to screen Create render texture > size Add render texture to camera Add render texture to material Now when you play the game the color correction takes effect. 



The bumpmap uses a normal map to indicate the high points and low points of an object using different rgb values that correspond to high (RGB = XYZ) | 0-255 = (-1) = (+1) in terms of slope.

To slightly modify this I decided to add a color change to the base color so I can change what the texture looks like.



The rimlight is a basic rimlight shader but I changed it so there was a central graduation instead of an actual rim. To do this I instead multiplied the saturated dot product of the normalized view direction and normalized object in world space.



Outline



I decided to add the outline to pac man to enhance the clarity on him with everything going on already in the scene. To do this I first had to cull the object in the front so the outline would only appear around the object. I then had transformed the object into clip space so I could then calculate the normals based on world position multiplied by UNITY\_MATRIX\_IT\_MV. I then added the offset position and multiplied it to finalise the outline location (makes it appear on the outside of the object). 



