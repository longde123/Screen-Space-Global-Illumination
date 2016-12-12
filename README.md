# Screen Space Global Illumination
The idea is simple, we sample some pixels from screen space as independent light sources, the light directions are their screen space normals, then we accumulate lights from them as global illumination for every pixel.

Because we are working in screen space, it support any light types and any number of lights.

Low resolution mode is where the magic is, I use small quads (32x32 pixels) to calculate global illumination, and sample in uniform grids of coordinates, since all calculations are in GPU, the speed is so fast that it always runs in realtime.

I also use blur passes to smooth the small depth quad, the small viewport quad and the small global illumination quad, the lighting looks more smoothly than ever.

Finally, I blend the global illumination to the original viewport.

That's all.

It can run on both desktop and mobile devices in realtime now!

This formula is used to calculate global illumination:

GI = lightColor * max(0, dot(lightNormal, lightToPixelNormal)) * max(0, dot(pixelNormal, pixelToLightNormal)) / Distance;

It is a simplified version of physics based global illumination.

### Screenshot
I use Urho3D game engine to test the effect, here is a screenshot:

![ssgi.jpg](http://www.mesh-online.net/ssgi.jpg)

Notice the color bleeding effect on the floor, the green curtain and the red cloth bled amazing colors on the floor, and the wood floor also bled soft colors on the green curtain.

### License
The MIT License (MIT)
