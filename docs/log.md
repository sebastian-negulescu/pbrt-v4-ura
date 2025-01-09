# Progress Log

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

