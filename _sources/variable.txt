Variable Density Flow
=====================

We study the solution of the Poisson equation in multi-material flows. The
following example shows a 1D problem in a domain :math:`[0,1]`, where the
unsimulated air phase occupies the region :math:`[0,0.1]`, incompressible water
phase occupies :math:`[0.1,0.6]\times[0.7,1]`, and an incompressible bubble phase occupies
:math:`[0.6,0.7]`.  ::

    import numpy as np
    import matplotlib.pyplot as plt
    from scipy.sparse import lil_matrix
    from scipy.sparse.linalg import spsolve
    
    cell_count = 100;
    pressure = [None]*cell_count;
    dx = 1./cell_count;
    
    # create flags
    flags = [None]*cell_count;
    for i in range(0,cell_count):
        location = (i+.5)*dx
        if(location>=0 and location<=.1):
            flags[i]=0;     # unsimulated air
        elif(location>.1 and location<=.6):
            flags[i]=1;     # water
        elif(location>.6 and location<=.7):
            flags[i]=2;     # bubble
        elif(location>.7 and location<=1):
            flags[i]=1;     # water
    
    # mark variables
    index=0
    variable_index = [None]*cell_count;
    for i in range(0,cell_count):
        if(flags[i]>0):
            variable_index[i]=index;
            index+=1;
        else: variable_index[i]=-1;
    
    number_of_dofs = index;
    density = [None]*cell_count;
    for i in range(0,cell_count):
        if(flags[i]==1):
            density[i]=10.;         # water
        elif(flags[i]==2):
            density[i]=1000.;       # bubble
        else: density[i]=0;
    
    face_weights = [None]*(cell_count-1);
    for i in range(0,cell_count-1):
        left_cell = i;
        right_cell = i+1;
        if(flags[left_cell]==0 and flags[right_cell]==0):
            face_weights[i]=0.;
        elif(flags[left_cell]==0 and flags[right_cell]==1):
            face_weights[i]=1./density[right_cell];
        else: face_weights[i]=2./(density[left_cell]+density[right_cell]);
    
    # create Poisson matrix
    A = lil_matrix((number_of_dofs,number_of_dofs));
    one_over_dx2 = (1./dx)*(1./dx);
    for i in range(0,cell_count):
        if(flags[i]>0):
            A[variable_index[i],variable_index[i]] += face_weights[i-1]*one_over_dx2;
            if(flags[i-1]>0): A[variable_index[i],variable_index[i-1]] -= face_weights[i-1]*one_over_dx2;
            if(i<cell_count-1):
                A[variable_index[i],variable_index[i]] += face_weights[i]*one_over_dx2;
                A[variable_index[i],variable_index[i+1]] -= face_weights[i]*one_over_dx2;
    A = A.tocsr()
            
    # create right hand side
    b = np.zeros(shape=(number_of_dofs,1))
    b[number_of_dofs-2] = 1.;
    
    # solve Ax = b
    x = spsolve(A,b);
    
    # output variables
    coord = [None]*cell_count;
    for i in range(0,cell_count):
        coord[i] = (i+.5)*dx;
        if(flags[i]==0): pressure[i]=0.;
        else: pressure[i]=x[variable_index[i]];
    
    plt.plot(coord,pressure,'ro')
    plt.show()
