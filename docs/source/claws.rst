Conservation laws and Domain meshing
====================================


The Time Step issue
-------------------
For an orthogonal or cartesian meshed domain  :math:`\Omega` , the Courant-Friedrichs-Levy criteria defines a CFL coefficient that linearly weights the time-step :

.. math::

  \Delta t_{x, y} &= CFL \frac{\Delta {x, y}} {\left| U_{x, y} \right|  + \sqrt{gh}}
 \\
 \\
  \Delta t &= min(\Delta t_x, \Delta t_y)_{\Omega}
 
And is applied to the mass conservation at every control-volume or cell, for instance in 1D(X):

.. math::

  \frac{\delta A} {\delta t} + \frac{\delta Q} {\delta x}=0 

Which can be discretized in an explicit way, like the Euler scheme :

.. math::

  \frac{ A^{n+1}_i - A^{n}_i} {\Delta t} + \frac{Q^{n}_{i-1/2}-Q^{n}_{i+1/2}} {\Delta x}=0 
  
Which allows for stability if  :math:`CFL \lt 1`

Whereas an implicit discretization scheme, like the box scheme:

.. math::

  \frac{ \left( \Psi A^{n+1}_{i-1} + (1-\Psi) A^{n+1}_i \right)- \left( \Psi A^{n}_{i-1} + (1-\Psi) A^{n}_i \right)} {\Delta t} + \frac{\Theta \left(Q^{n+1}_{i-1}-Q^{n+1}_{i}\right)+(1-\Theta)\left( Q^{n}_{i-1}-Q^{n}_{i}\right)} {\Delta x}=0 
  
With  :math:`0 \le \Psi \le 1` and :math:`0 \le \Theta \le 1` allows for stability even with :math:`CFL \gt 1`

The price for an implicit scheme, as briefly seen, is that the solving algorithm and coding are more complex but the execution can be faster, depending also on the domain mesh division and its hardware distribution among processing units (CPU, GPU or TPU).
Particularly, the popular HEC-RAS code uses an implicit scheme formulation.

Note we did not consider the conservation of momentum, for the sake of simplicity in the formulation.
To know more visit:
