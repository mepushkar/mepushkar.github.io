---
layout: post
title: 25 Line FEM code for Bar subjected to point load at free end and clamped at another
subtitle: :stuck_out_tongue_winking_eye: FEM in Python :stuck_out_tongue_winking_eye:
cover-img: /assets/img/Python-Symbol.png
gh-badge: [star, fork, follow]
comments: true
---
Just for fun


import numpy as np
import matplotlib.pyplot as plt

nelm = 5; le = 1/nelm;
kloc = np.array([[1,-1],[-1,1]])
a = np.array(list(range(0,nelm)))
icon = np.empty((nelm,2), dtype = np.int8)
icon[:,0] = a 
icon[:,1] = a+1
nnod = nelm+1;
kg = np.zeros((nnod,nnod));
fg = np.zeros(nnod)
x = np.linspace(0,1,nelm+1);
for i in range(0,nelm):
    n1 = icon[i][0]; n2 = icon[i][1];
    x1 = x[n1]; x2 = x[n2];
    iv = np.array([n1,n2])
    kg[iv[:,None],iv] += (kloc/le)
kg[0,:] = 0; kg[:,0] = 0; kg[0,0] = 1;
fg[:,None] = fg[:,None]-np.reshape(kg[:,0],(nelm+1,1))*0 
fg[-1] = 1;
u = np.linalg.solve(kg,fg)
plt.plot(x,u*0,"r*-")
plt.plot(x+u,x*0,"bo--")
plt.xlabel("Descritization along X")
plt.ylabel("Displacement u")
plt.legend(["undeformed","deformed"])
plt.show()
}

