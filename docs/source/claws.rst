Conservation laws and Domain meshing
====================================


The Time Step issue
-------------------
For an orthogonal or cartesian meshed domain &#937; 

.. math::

  \Delta t_{x, y} &= CFL \frac{\Delta l_{x, y}} {\left| U_{x, y} \right|  + \sqrt{gh}}
 \\
 \\
  \Delta t &= min(\Delta t_x, \Delta t_y)_{\Omega}
 
Is applied to the mass conservation:
.. math::

  \frac{\partial A} {\partial t} + \frac{\partial Q} {\partial x}=0 

