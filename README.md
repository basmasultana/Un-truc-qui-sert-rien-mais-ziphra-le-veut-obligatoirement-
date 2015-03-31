# Un-truc-qui-sert-rien-mais-ziphra-le-veut-obligatoirement-
#Je l'ai trouvé sur internet mais ca marche pas!
from __future__ import division
from pylab import *
from scipy import *
from scipy.integrate import odeint
import os

#initialisation
g = 10
alpha = pi/4
v0 = 10
x_ini, y_ini = 0, 0
vx_ini, vy_ini = v0*cos(alpha), v0*sin(alpha)
tini = 0
tfin = 2
Npas = 50

def F(Y, t):
    [x,  vx, y, vy] = Y
    eq1 = vx
    eq2 = 0
    eq3 = vy
    eq4 = -g
    return [eq1, eq2, eq3, eq4]

cond_ini = [x_ini, vx_ini, y_ini, vy_ini]
t = linspace(tini, tfin, Npas)
Yn = odeint(F, cond_ini, t)
[x, vx, y, vy] = Yn.T

# Construction d'une sÃ©rie d'images et de leur assemblage dans une animation
Xcadre_min = min(x)*1.1
Xcadre_max = max(x)*1.1
Ycadre_min = min(y)*1.1
Ycadre_max = max(y)*1.1
for k in range(Npas):
    plot(x[k], y[k], 'o', color='b')
    axis([Xcadre_min, Xcadre_max, Ycadre_min, Ycadre_max], aspect='equal')
    filename = 'fichierTemp'+str('%02d' %k)+'.pdf'
    savefig(filename)
    print ('Nplot = ',  k)
