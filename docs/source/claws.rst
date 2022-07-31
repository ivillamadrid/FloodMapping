Conservation laws and Domain meshing for numerical simulations
==============================================================


Type of mesh
------------

.. image:: TriangularMeshes.png
  :width: 400
  :alt: Typical triangular based meshes


Triangular based meshes for 2D domains, to discretize the mass and momentum differential equations.

Practical approach: hybrids
===========================
The river main channel interaction with the floodplain by overtopping embankments or levees can be modelled using a combination of cells (quadrilateral or triangular) wich will require higher density of cells in the transitions or when the speed pattern is expected to be more complex or less uniform in space. The whole domain can be seen as a 1D conduit plus a 2D plain or as a whole 2D domain.


For instance RSH-2D (US Bureau of Reclamation, 2008) combines quadrilateral cells along the main channel and levees but mixed coarser cells at the plains.
.. image:: SRH-Hybrid.png
  :width: 400
  :alt: SRH

Mass and momentum conservation
-------------------------------


The Time Step issue
-------------------
For an orthogonal or cartesian meshed domain  :math:`\Omega` , the Courant-Friedrichs-Levy criteria defines a CFL coefficient that linearly weights the time-step :

.. math::

  \Delta t_{x, y} &= CFL \frac{\Delta {x, y}} {\left| U_{x, y} \right|  + \sqrt{gh}}
 \\
 \\
  \Delta t &= min(\Delta t_x, \Delta t_y)_{\Omega}

Note that if :math:`(\Delta {x, y}\ll, U_{x, y}\gg, h\gg )\Longrightarrow \Delta t \rightarrow 0`

The time-step governs the mass conservation at every control-volume or cell, for instance in 2D(X, Y):

.. math::

  \frac{\delta h} {\delta t} + \frac{\delta (hU_x)} {\delta x}+ \frac{\delta (hU_y)} {\delta y}=0 

Whereas we go deeper with the simpler 1D(X) formulation:

.. math::

  \frac{\delta A} {\delta t} + \frac{\delta Q} {\delta x}=0 

Which can be discretized (super-index 'n' stands for evolution in time and sub-index 'i' for location in 1D-grid) in an explicit way, like the Euler scheme :

.. math::

  \frac{ A^{n+1}_i - A^{n}_i} {\Delta t} + \frac{Q^{n}_{i+1/2}-Q^{n}_{i-1/2}} {\Delta x}=0 

Called explicit because the value at 'n+1' can be formulated joining only known terms at 'n' on the right hand side:

.. math::

  A^{n+1}_i =  A^{n}_i+ \frac{\Delta t}{\Delta x} \left( Q^{n}_{i-1/2}-Q^{n}_{i+1/2} \right) 

Which allows for stability if  :math:`CFL \lt 1`

Whereas an implicit discretization scheme, like the box-scheme:

.. math::

  \frac{ \left( \Psi A^{n+1}_{i+1} + (1-\Psi) A^{n+1}_i \right)  - \left( \Psi A^{n}_{i+1} + (1-\Psi) A^{n}_i \right)} {\Delta t} +\\
  \frac{\Theta \left(Q^{n+1}_{i+1}-Q^{n+1}_{i}\right)  + (1-\Theta)\left( Q^{n}_{i+1}-Q^{n}_{i}\right)} {\Delta x}=0 
  
With  spatial weight :math:`0 \le \Psi \le 1`, and implicit parameter :math:`0 \le \Theta \le 1` allows for stability even with :math:`CFL \gt 1`

The price for an implicit scheme, as briefly seen, is that the solving algorithm and coding are more complex but the execution can be faster, depending also on the domain mesh division and its hardware distribution among processing units (CPU, GPU or TPU).
Particularly, the popular HEC-RAS code uses an implicit scheme formulation.

Note we did not consider the conservation of momentum, for the sake of simplicity in the formulation.
To know more visit[]

Simulation mass balance
-----------------------

One overall value to check at the end of every simulation is the mass conservation applied to the entire domain for accounting the difference of volume, and all the inflows and outflows across the boundaries.

.. math::

  V^{T} -V^{0} =  \sum_k{Q^k_{in} \Delta t_k} - \sum_k{Q^k_{out} \Delta t_k}
 
Where

.. math::

  V^{n}=\sum_{\Omega}h^n_{ij}\delta x_i \delta y_j 
