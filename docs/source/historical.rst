Historical reviews
==================

As stated by `Stoker`_ , in "Water Waves: The Mathematical Theory with Applications", since 1957 it is clear and feasible to make predictions of floods in rivers knowing the state of the river at some initial instant,
and the observed-estimated or forecasted, flow into the river from its tributaries and the local run-off, through the basic differential equations we have roughly presented, and their associated numerical solutions solved by computers.


After more than 60 years of Stoker practices, the digital era with open access RS data and affordable computing processors, has popularized the Flood-Mapping science, a state of the art methodology can be found in "Flood Inundation Prediction" by `Bates, 2022`_, being the main challenges to face: 

* Rationalize and properly select among the considerable bulk of observational data, including the imagery to validate predictions.

* Match the numerical engine which describes best the physical process, to the available terrain model (resolution and accuracy) and temporal scales, assuming the computational cost. In general relaxing the grid resolution to coarse pixels, allows to validate more parameters and scenarios, that for large scale hazard mapping related to Climate Change is very relevant, but non-appropriate for local hydraulic modelling.

.. _Stoker: https://doi.org/10.1002/9781118033159

.. _Bates, 2022: https://doi.org/10.1146/annurev-fluid-030121-113138


Scanned images
--------------

Flood modelling is not only about choosing an appropriate mesh and numerical solver, the topology and connections between hydraulic structures play a major role, we rediscover here the concept of "breakline" for the river axis and its flow distribution across plain cells,  by Giammarco and Todini, 1994, when numerical engines started to couple with Geographical Information Systems or GIS frameworks.

.. image:: BreakLine_FloodPlain_Giammarco-Todini_1994.jpg
  :width: 400
  :alt: Giammarco-Todini_1994.

