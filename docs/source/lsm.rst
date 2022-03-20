Large Scale Modelling assisted by Satellite imagery and Artificial Intelligence
===============================================================================

While monitoring large areas or tiles of several hundred Kilometers, with pixel size over 25 meters, 
it is convenient to reduce the complexity of the shallow water equations (SWE) in order to allow larger 
time-steps for numerical simulations at the expense of loosing accuracy for the speed field pattern or wave propagation time.
The objective for Large Scale Modelling (LSM) is to maintain critical information like the maximum flood extent and its duration, but none about highly transient states nor dynamics related to fine grid resolutions: trans-critical flows, overtopping, sediment transport and bed river evolution, pollutant dispersion, etc.
 
Difussion-Wave or Zero-Inertia approximation
---------------------------------------------

The momentum conservation at every control-volume or cell for the full (or complete) SWE equations, 1D(X) case, states:

.. math::

  \frac{\delta Q} {\delta t} + \frac{\delta \left( Q^2/A \right)} {\delta x} = gA \frac{\delta \left( Z_b+h \right)} {\delta x}-S_f 

Can be adapted (or adopted) for LSM considering the inertial (or acceleration) terms vanish:

.. math::

  \frac{\delta Q} {\delta t} \rightarrow 0 \\
  \frac{\delta \left( Q^2/A \right)} {\delta x} \rightarrow 0 \\
  
Or equivalently:

.. math::

  S_f = gA \frac{\delta \left( Z_b+h \right)} {\delta x}\\


That links, using Manning´s friction formulation, the intercell discharge 'Q' to the gradient of stage or water-elevation. 

An interesting implicit version of the equation is used by Lisflood-FP [Neal et al., 2012]:

.. math::

 q^{n+1}_{i+1/2} =  \frac{q^n_{i+1/2} -g h^n_f \Delta t \grad(Zb+h)}{1+g \Delta t n^2 \frac{ \left|q^n_{i+1/2}\right|}{(h^n_f)^{7/3}}  


