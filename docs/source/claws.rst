Conservation laws and Domain meshing
====================================


The Time Step issue
-------------------
For an orthogonal or cartesian meshed domain  :math:`\Omega`

.. math::

  \Delta t_{x, y} &= CFL \frac{\Delta {x, y}} {\left| U_{x, y} \right|  + \sqrt{gh}}
 \\
 \\
  \Delta t &= min(\Delta t_x, \Delta t_y)_{\Omega}
 
Is applied to the mass conservation at every control-volume or cell, for instance in 1D(X):

.. math::

  \frac{\delta A} {\delta t} + \frac{\delta Q} {\delta x}=0 

Which can be discretized in an explicit way, like :

.. math::

  \frac{ A^{n+1}_i - A^{n}_i} {\Delta t} + \frac{Q^{n}_{i-1/2}-Q^{n}_{i+1/2}} {\Delta x}=0 
  
Which allows for stability if :math:`CFL \lt 1`

Whereas an implicit discretization scheme like the box scheme:

.. math::

  \frac{ \Theta \left( A^{n+1}_{i+1} - A^{n+1}_i \right)+ (1-\Theta)\left( A^{n}_{i+1} - A^{n}_i \right)} {\Delta t} + \frac{\Psi \left(Q^{n+1}_{i-1}-Q^{n+1}_{i}\right)+(1-\Psi)\left( Q^{n+1}_{i-1}-Q^{n+1}_{i}\right)} {\Delta x}=0 
