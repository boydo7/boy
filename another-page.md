---
layout: default
---

## Inversion model for geophysics

```
Created on Fri Apr  1 00:36:28 2022

@author: Boydo
"""
#Bidang Refleksi

import numpy as np
import matplotlib.pyplot as plt

#masukkan data
a = np.array([60, 80, 100, 120, 140, 160, 180, 200])
b = np.array([0.5147, 0.5151, 0.5155, 0.5161, 0.5167, 0.5175, 0.5183, 0.5192])

#proses inversi
n = len(a)
G = np.ones((n,2))
d = np.ones((n,1))
for i in range (n):
    G[i,1] = a[i]**2
    d[i,0] = b[i]**2
Gt = np.transpose(G)
GtG = Gt.dot(G)
GtGi = np.linalg.inv(GtG)
Gtd = Gt.dot(d)
m = GtGi.dot(Gt).dot(d)

#membuat persamaan
x = np.linspace(0,250,1000)
y = np.sqrt(m[0,0] + m[1,0]*x**2)

#membuat grafik
fig, ax = plt.subplots()
plt.plot(a,b,'ro',label='Observasi')
plt.plot(x,y,label='Model ')
ax.set(xlabel='offset (meter)', ylabel='Travel Time (detik)',
       title='Offset vs Travel Time')
ax.grid()
plt.axis([min(x), max(x), max(y),min(y)])
ax.legend(loc='lower right')
plt.show()

print (d)

```



[back](./)
