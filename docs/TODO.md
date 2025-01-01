# TODO

## Project Direction

Two ways we can go:
- Focus on Sodium Chloride
    - Requires a re-write of the Integrator to not consider interactions within the medium
- Focus on phase function comparisons
    - Keep the Volumetric Integrator already defined
    - Use a more common substance like seawater or distilled water

I am more partial to the second way, that doesn't involve rewriting and entire Integrator.
So, what would we need? Both the absorption and scattering coefficients of either seawater or distilled water.

Interestingly, there's a "Pacific Ocean Surface Water" scattering property baked into PBRT
that gives an absorption and scattering coefficient.
I should probably find my own scattering coefficients to use.

Also, with this second way, we can include more phase functions like Mie and Rayleigh.

