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

It is a relatively easy way of processing and detecting water surfaces over a certain "MNDWI" threshold value, coping with bimodal pixel distributions and the Otsu optimal threshold, in fact the problem is to detect accurately the dry-wet boundaries, and there the computational vision techniques for noise filtering and edge detectors play a major role. See the practical case with Google-Earth-Engine for `Paso de las Piedras`_ reservoir, Bahía Blanca, Argentina.

.. _Paso de las Piedras: https://www.researchgate.net/publication/357174237_Prototipo_Google-Earth-Engine_para_el_modelado_hidrologico_del_embalse_Paso_de_Las_Piedras_Argentina

Image processing: noise filtering
---------------------------------
Multi-Spectral and Panchromatic imagery are subject to the presence of cloud cover, whereas SAR microwaves are not perturbed. For the former group
access to pre-event images or filtering techniques are needed. The presence of vegetation over water bodies is a common and frequent source of noise for any exploitation of remote sensing imagery. 
SAR imagery researchers and practitioners continue improving algorithms to identify water bodies under vegetation or between buildings, considering effects like double bounce and shadows for the backscatter, that depend on the wave-length, polarisation and incidence angle, and of course the surface roughness and dielectric properties, but those SAR processing  techniques are out of the scope of this basic manual, and usually deal with segmentation, supervised or trained classifiers within Deep-Learning frameworks, and multi-temporal sequences of images.

Image processing: edge detectors and buffers
--------------------------------------------
To locate the wet-dry boundaries a 2D convolution operator is set to identify that particular pattern across the domain, this is an image processing technique commonly used, that for every pixel of the domain weights the surrounding pixels according to a defined Kernel.
For instance to detect a North dry-wet edge, a 3x3 kernel can be set to {[1, 1, 1], [-1, -1, -1 ], [0, 0, 0]} and subsequently applied to a MNDWI or back-scatter water surface layer,  to detect negative values below a threshold which are candidates to represent a North dry-wet bound. 

The following image summarizes the action of a Kernel (Sobel-Gaussian) filtering over a source image:

.. image:: Convolution-2D_Kernel-SobelGx.png
  :width: 400
  :alt: Convolution


In order to estimate the water depth related to the water surface recorded by satellite imagery (with no altimetry, ie Multi-Spectral or SAR backscatter), a base DTM or raster elevation is needed, where the 2D-convolution operator is applied using a Kernel that weights the terrain neighbours to have a mean value of the bottom, adding a special treatment to have extra-accuracy at dry-wet boundaries, river banks or embankments, to serve as reference for the water surface height. 


AI to train and validate global surface water mapping
-----------------------------------------------------
See for more details the `JRC database`_ .
 
.. _JRC database: https://developers.google.com/earth-engine/datasets/catalog/JRC_GSW1_3_GlobalSurfaceWater?hl=en 



