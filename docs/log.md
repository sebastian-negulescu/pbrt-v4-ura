# Progress Log

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

