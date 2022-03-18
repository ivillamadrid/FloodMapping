Conservation laws and Domain meshing
====================================


The Time Step issue
-------------------
For an orthogonal or cartesian meshed domain  :math:`\Omega`

.. math::

  \Delta t_{x, y} &= CFL \frac{\Delta l_{x, y}} {\left| U_{x, y} \right|  + \sqrt{gh}}
 \\
 \\
  \Delta t &= min(\Delta t_x, \Delta t_y)_{\Omega}
 
Is applied to the mass conservation at every control-volume or cell, for instance in 1D-X:

.. math::

  \frac{\delta A} {\delta t} + \frac{\delta Q} {\delta x}=0 

Which can be discretized in a explicit way, like :

.. math::

  \frac{ A^{n+1}_i - A^{n}_i} {\delta t} + \frac{Q^{n}_{i-1/2}-Q^{n}_{i+1/2}} {\delta x}=0 
