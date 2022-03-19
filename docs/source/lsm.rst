Large Scale Modelling assisted by Satellite imagery and Artificial Intelligence
===============================================================================

While monitoring large areas or tiles of several hundred Kilometers, with pixel size over 25 meters, 
it is convenient to reduce the complexity of the shallow water equations (SWE) in order to allow larger 
time-steps for numerical simulations at the expense of loosing accuracy for the speed field pattern or wave propagation time.
The objective for Large Scale Modelling (LSM) is to maintain critical information like the maximum flood extent and duration, but no dynamics related to
fine grid resolutions, like trans-critical flows, overtopping, sediment transport and bed river evolution, pollutant dispersion, etc.
 
Difussion-Wave or Zero-Inertial approximation
---------------------------------------------

The momentum conservation at every control-volume or cell, for instance in 1D(X):

.. math::

  \frac{\delta Q} {\delta t} + \frac{\delta Q^2/A} {\delta x} = \frac{\delta Z_b} {\delta x}-S_f 

Can be simplified as:
