Large Scale Modelling assisted by Satellite imagery and Artificial Intelligence
===============================================================================

While monitoring large areas or tiles of several hundred Kilometers, with pixel size over 25 meters, 
it is convenient to reduce the complexity of the shallow water equations (SWE) in order to allow larger 
time-steps for numerical simulations at the expense of loosing accuracy for the speed field pattern or wave propagation time,
The objective for LSM is to maintaining critical information like the maximum flood extent and duration, but no facts related to
fine grid resolutions, like trans-critical flows, overtopping details, sediment transport and bed river evolution, etc.
 
Difussion-Wave or Zero-Inertial approximation
---------------------------------------------

The momentum conservation at every control-volume or cell, for instance in 1D(X):

.. math::

  \frac{\delta Q} {\delta t} + \frac{\delta Q^2/A} {\delta x} = \frac{\delta Z_b} {\delta x}-S_f 

Which can be simplified as:
