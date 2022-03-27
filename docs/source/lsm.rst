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

.. list-table:: 
   :widths: 10 20 10 20
   :header-rows: 1

   * - Symbol
     - Variable and dimension
     - Symbol
     - Variable and dimension
     
   * - Q
     - discharge (m^3/s), Q=Av
     - A
     - area      (m^2)
   * - Zb
     - bed level (m)
     - h
     - water depth (m)
   * - Sf
     - friction slope (m^3/s^2)
     - g
     - gravity constant (m/s^2)

Can be adapted (or adopted) for LSM considering the inertial (or acceleration) terms vanish:

.. math::

  \frac{\delta Q} {\delta t} \rightarrow 0 \\
  \frac{\delta \left( Q^2/A \right)} {\delta x} \rightarrow 0 \\
  
Or equivalently:

.. math::

  S_f = gA \frac{\delta \left( Z_b+h \right)} {\delta x} \equiv gA \nabla (Z_b+h)\\


That links friction slope with stage gradient. Using empirical Manning´s formulation with 'n' as roughness coefficient,  1D(X) or 2D(X, Y):

.. math::

  S_{f}=n^2 \frac{Q \left| Q \right| }{A^2 R^{4/3}}, \;
  S_{f x, y}=n^2 \frac{U_{x, y} \sqrt{U^2_x+U^2_y} }{h^{4/3}} 


allows to define the intercell discharge 'q'. For instance, the 2D code Lisflood-FP uses

.. math::

 q^{n+1}_{i+1/2} =  \frac{(h^n_f)^{5/3}}{n} \nabla(Z_b+h^n)^{1/2}_{i+1/2}  


With the flow-depth  as

.. math::

 h^n_f=max \left( (Z_b+h^n)_i, (Z_b+h^n)_{i+1}\right)-max \left((Z_b)_i, (Z_b)_{i+1} \right)
 
And an interesting implicit version 

.. math::

 q^{n+1}_{i+1/2} =  \frac{q^n_{i+1/2} -g h^n_f \Delta t \nabla(Z_b+h^n)_{i+1/2}}{1+g \Delta t \frac{n^2  \left|q^n_{i+1/2}\right|}{(h^n_f)^{7/3}}}  



See for more details `Neal et al, 2012`_ .

.. _Neal et al, 2012: https://doi.org/10.1029/2012WR012514

Satellite Optical and IR bands to detect water bodies: MNDWI index
-------------------------------------------------------------------

The combination of bands that defines the Modified Normalized Difference Water Index (MNDWI) is visible green (537-582 nm) and short-wave infrared (1539-1681 nm), that in case of the Sentinel-2 MSI are B3 and B11 respectively:

.. math::

 MNDWI=\frac{B_3-B_{11}}{B_3+B_{11}}
 
 
See for more details `Cordeiro et al, 2021`_ .
 
.. _Cordeiro et al, 2021: https://doi.org/10.1016/j.rse.2020.112209 

Image processing: noise filtering
---------------------------------

Image processing: edge detectors and buffers
--------------------------------------------

In order to estimate the water depth related to the water surface recorded by satellite imagery (with no altimetry, ie Multi-Spectral or SAR backscatter), a base DTM is needed.


AI to train and validate global surface water mapping
-----------------------------------------------------
See for more details the `JRC database`_ .
 
.. _JRC database: https://developers.google.com/earth-engine/datasets/catalog/JRC_GSW1_3_GlobalSurfaceWater?hl=en 



