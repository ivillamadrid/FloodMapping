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
 
Is applied to the mass conservation at every control-volume or cell:

.. math::

  \frac{\delta A} {\delta t} + \frac{\delta Q} {\delta x}=0 

