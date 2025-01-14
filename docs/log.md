# Progress Log

## Jan. 13

Need to make a "directional" area light.

## Jan. 10

Today, we figure out how to get point lights to refract properly.
Nope.
Today, we look at some solutions to get point lights to refract properly.

There are three solutions that I thought up:
- Propagate light sampling to transmission rays too 
- Use a spherical light and a lens to refract rays in a parallel direction
- Use a directional light and a wall to block all light but a few controlled rays.
    This might not work.

## Jan. 9

:facepalm: I figured out the setting for the maximum bounces a ray can take.
The default is 5 and I've been rocking with that for some unknown reason.
This setting solves all the problems I've been having and it only took 4 days to find.
For some reason I thought they'd use russian roulette termination to probabalistically
extinguish a ray once its light contribution got smaller,
but I think it's a mix of both.
The performance hit of cranking the max depth is not bad which makes me think
that there is also some other criteria for ray termination.
This was a good discovery though, 
now we can move on to scattering and see if that helped anything.

Refraction with non-area lights is still broken,
even though the scattering works.
Need to see how refractions are implemented and if we can get it to work.

## Jan. 8

Yesterday, I made my own cuvette model manually.
This brought both some problems and solutions.
It solved the issue of symmetrical scattering with the other cuvette.
But, I can't tell if it's still off or the reflection is weird.

## Jan. 7

I made two tesseracts (cuvettes) today: 
- one with a cube inside a cube that has no edges connecting the cubes
- another that is made up of six 3D trapezoids? all rotated and translated together

Using the second is definitely the way to go,
as the first does not properly work with dielectrics.
I would like to try it again sometime, as I think it is cleaner,
but for now it is best to use the one made from multiple well-defined components.

The behaviour of mediums is still weird to me.
I need to check out what is being set to the inside medium and what is being set to the outside.
Currently, what I think is the inside medium does not scatter light coming from
point lights,
it only scatters light from area lights.

Checked the source code, first parameter is the inside medium, second parameter is the outside medium.
This is really weird to me that the second parameter would better scatter than the first.

## Jan. 6

Set up a test scene to test if the phase functions are working as expected.
This scene adapts the simple scene from [PBRT v4's user guide](https://pbrt.org/fileformat-v4#example).
Phase functions work fine in mediums if these mediums are standalone.
If I try to make the material of the medium's shape a dielectric,
the scattering observed from non-area lights disappears.

I'll have to take a look at how mediums fill their respective shapes,
as it is odd that a dielectric material filled with a homogeneous medium
does not scatter any light.
Maybe, since the ray passing through the medium will be a dielectric ray,
it does not sample the non-area light.
The reasoning for this would be that a regular dielectric would not need to
directly sample the light as a person cannot physically "see" the light,
only the bounces of it.

To combat this, I will not apply mediums to shapes,
I will make the shapes hollow and create a standalone medium within.
Let's try adding this to the test scene tomorrow.

