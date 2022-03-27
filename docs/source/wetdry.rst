Wet-Dry front dynamics
======================


The Dam-Break problem or the breaking of a dam (Stoker, 1957, 1D) tracks the evolution of a reservoir and a downstream water column, both steady and with different heights initially, over ideal bottom conditions; flat and frictionless bed. Stoker showed there is an analytical or exact solution for the moving front: a simple "parabolic curve" when the downstream area is dry, and a more complex one when the downstream area is wet: [see figures]


Both problems are a good introduction to visualize the flooding dynamics of shallow water waves, although the complexity grows while natural conditions like irregular bottom (change of slopes) and friction or dissipation are considered. To solve "approximately" now the front evolution and flood extent we need to discretize the mass conservations equations and apply numerical algorithms crunched by computer power, once the bottom is known (think of a digital elevation model) and the boundary conditions are known (think of measured inflows and outflows)

At this early point it is important to think if your study case will need to evaluate the whole dynamics, with fronts or discontinuities moving across the domain of interest, with an accurate speed distribution, or just mean water depth values and maximum flood extents that can be solved with simplified schemes that are not so CPU demanding.

.. image:: /.png
  :width: 400
