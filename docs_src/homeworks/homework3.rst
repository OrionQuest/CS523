Homework #3
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    Consider a uniform :math:`N\times N` grid whose bottom left node is at the
    point :math:`(-0.5,-0.5)` and top right node is at the point :math:`(0.5,0.5)`.
    Define a circle :math:`C` centered at :math:`(0,0)` and with radius
    :math:`0.25`. Label all voxels inside :math:`C` as *Interior*, and
    all other voxels as *Dirichlet*. Use the analytic function :math:`\phi=x^2 +
    y^2 - r^2` to define the Dirichlet values. However, as pointed out in class,
    for each Dirichlet voxel, project its cell center to the *nearest* point on
    the circle, compute the :math:`\phi`-value at that point, and use this as
    the Dirichlet value for the cell. In other words, if :math:`p` is the
    location of the cell center of a Dirichlet voxel, compute the point :math:`q=0.25*p`, and use the
    :math:`\phi`-value at :math:`q` for the Dirichlet value at :math:`p`.
    Set the right hand side to be the constant :math:`4` for each voxel.

    Using the methology discussed in class, write a :math:`\textsf{CG_System}`
    class and a :math:`\textsf{CG_Vector}` class, and solve the Poisson equation
    for the setup described above using :math:`\textsf{Conjugate Gradients}`.
    Report the :math:`L_\infty`-norm for the *error* computed as
    :math:`|\phi_\texttt{cell} - x^2 - y^2 + r^2|` for each voxel, for grids
    :math:`16\times16`, :math:`32\times32`, :math:`64\times64`, :math:`128\times128` and
    :math:`256\times256`. If your solution is correct, you should see the error
    decrease approximately by a factor of :math:`2` each time you double the
    grid resolution. Compute the *order of convergence*, defined as
    :math:`\log_2(e_{N\times N}/e_{2N\times2N})`, where :math:`e_{N\times N}`
    is the :math:`L_\infty`-norm of the error for an :math:`N\times N` grid.

    **Note:** Please follow the implementation of :math:`\textsf{Conjugate_Gradient}`
    as described `here <https://github.com/OrionQuest/Nova/blob/master/Library/Tools/src/Krylov_Solvers/Conjugate_Gradient.cpp>`_
    to make use of the :math:`\textsf{CG_System}` and :math:`\textsf{CG_Vector}` classes.
