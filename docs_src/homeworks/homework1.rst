Homework #1
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    The *Lotka-Volterra model* for the predator-prey problem comprises of the
    following system of ordinary differential equations

    .. math::
        \dot{u} = u(v-2) \\
        \dot{v} = v(1-u)

    .. image:: ../images/PP_FE.png
        :height: 600px
        :width: 800px
        :scale: 75%
        :align: center

    Python code for a forward Euler discretization of the above system with a time step size
    of :math:`\Delta t = 0.12` is given below, and generates the plot shown above. ::

        import matplotlib.pyplot as plt

        u = [2]
        v = [2]
        h = .12
        for i in range(1,100):
            u_new = u[i-1] + h*u[i-1]*(v[i-1]-2.)
            v_new = v[i-1] + h*v[i-1]*(1.-u[i-1])
            u.append(u_new)
            v.append(v_new)

        plt.plot(u,v,'ro')
        plt.axis([0,6,0,10])
        plt.show()

    Using the same time step size of :math:`\Delta t = 0.12`, compute the plots for a backward Euler
    discretization (with an initial guess of :math:`(4,8)`) and a symplectic Euler discretization (with two different initial guesses :math:`(4,2)` and :math:`(6,2)`)
    of the above system of equations.

.. topic:: Problem 2

    Implement a rigid body simulator for a freely falling object with some
    initial angular velocity and upward linear velocity. (Please do not use a sphere,
    so that the effect of rotations is clearly visible.)
