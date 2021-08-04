import numpy as np
from numpy import pi
import matplotlib.pyplot as plt
from configparser import ConfigParser


#Carga los valores de lamda, numero de iteraciones, y las condiciones iniciales s0 y t0 de CondicionesIniciales.py


parser = ConfigParser()
parser.read('Entradas.ini') 

lamda = parser.getfloat('Parametros','lamda')
n = parser.getint('Parametros','n')

t0 = parser.getfloat('CondicionesIniciales','t0')
s0 = parser.getfloat('CondicionesIniciales','s0')




W=1.e-10

G=lamda*np.log(32./W)

ss = np.zeros(n) 	#vectores para luego graficar
tt = np.zeros(n)
tt2 = np.zeros(n) 
ss2 = np.zeros(n)
delta = np.zeros(n)



t = t0
s = s0

d0 = 1.e-9

s2 = s0 + d0
t2 = t0 + d0



for i in range(n):
	s = s - np.sin(t)
	t = t-lamda*np.log(np.absolute(s))+G
	t = np.mod(t,2*pi)	#para que sea periodico en 2pi
	if t<-pi:			#porque t esta en (-pi,pi)
		t = t + 2*pi
	elif t>pi:
		t = t - 2*pi
	ss[i] = s
	tt[i] = t
	
	s2 = s2 - np.sin(t2)
	t2 = t2 - lamda*np.log(np.absolute(s2))+G
	t2 = np.mod(t2,2*pi)
	
	if t2<-pi:
		t2 = t2 + 2*pi
	if t2>pi:
		t2 = t2 - 2*pi
		
	ss2[i] = s2
	tt2[i] = t2

	delta[i]=np.sqrt((s-s2)**2+(t-t2)**2)

x=np.linspace(1,n,n)


plt.figure()
plt.plot(tt,ss,'.',markersize='0.5',color='k')			
plt.xlim(-pi,pi)
plt.ylim(-12,12)
plt.title('Whisker Mapping.'+r'$\lambda$='+str(lamda)+r' $t_0$='+str(t0)+r'. $s_0$='+str(s0))
plt.xlabel('t')
plt.ylabel('s')

plt.savefig('WM_'+'lamda='+str(lamda)+'t0='+str(t0)+'_s0='+str(s0)+'.png')
plt.show()
		
		
plt.figure()
plt.plot(x,delta,color='k')			
plt.xlim(0,n)

plt.title('Delta. t0='+str(t0)+'. s0='+str(s0))
plt.savefig('Delta.t0='+str(t0)+'_s0='+str(s0)+'.png')

plt.xlabel('n')
plt.ylabel(r'$\delta$(n)')
