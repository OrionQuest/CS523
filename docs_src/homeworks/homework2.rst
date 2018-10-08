Homework #2
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    Given an input shape, specified using an analytic signed distance function, store
    it as a discrete signed distance function on the nodes of a uniform Cartesian grid.
    Then, given a random point in space, write routines to:

    * identify whether the point is inside or outside the shape, and
    * project the point to the closest point on the surface of the shape. (Note
      that this may require few iterations to ensure convergence. At each step,
      you should compute the normal, and move the point by an amount equal to
      its distance value along the normal direction.)

    Test your code for three different shapes (such as a circle, ellipse, and
    square) both in 2D and in 3D. Use 10 points chosen uniformly at random for
    each problem.

.. topic:: Problem 2

    Using your solution to Problem 1, implement the collision
    detection/resolution algorithm from `this paper <https://www.cs.ubc.ca/~rbridson/docs/rigid_bodies.pdf>`_ (see Section 6) in your rigid body simulator designed in Homework #1.
    You may also want to consult `these notes <https://www.cs.cmu.edu/~baraff/sigcourse/notesd2.pdf>`_ for a more detailed
    explanation.
