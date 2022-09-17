Digital Elevation Models
========================


Common sources and vertical accuracy
------------------------------------


.. image:: VAccuracy-Scales_Schumann-Bates_2018.jpg
  :width: 400
  :alt: Vertical accuracy, scales and common techs.

DEMs: spatial resolution and vertical accuracy for different RS techniques and scales of application. From `Schumann & Bates, 2018`_

.. _Schumann & Bates, 2018: https://doi.org/10.3389/feart.2018.00225


DSM filtering to obtain DTM
---------------------------

.. image:: DSM_DTM_Guth_et_al_2021.png
  :width: 600
  :alt: DSM & DTM.
  
 
Digital Surface Model versus Terrain Model in "Terminology and Definitions for Digital Elevation Models", `Guth et al, 2021`_.

.. _Guth et al, 2021: https://doi.org/10.3390/rs13183581 

To understand how to transform a DSM from a Remote-Sensing device, as simple and affordable as a drone camera, in optical range (no LiDAR nor laser detection),
we describe the principles to generate a cloud of points from geo-referenced pictures, the 3D building of the surface model and the filtering with SMRF (Simple Morphological Filter) to remove basically the vegetation and blocks: 



Training with affordable drones
-------------------------------

In this section we practice with High-Quality drone imagery and the Open-Drone-Map software (`ODM`_), to obtain DSMs and DTMs from simple flights to 
set the essential ground data for reliable simulations, at scales of a few hectares.

.. _ODM: https://opendronemap.org/'




