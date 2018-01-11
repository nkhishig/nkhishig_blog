
## Rigid Body Collision Theory  

For two rigid bodies in collision the equations of motion are determined using the concept of impulse. We make the assumption that the collision happens quickly enough that there is no change in the position or orientation of the bodies. Also we do not account for friction when computing the forces in the system, allowing only the force in the direction perpendicular to the edge of the bodies during the collision, noted by the unit vector $$\vec{n}$$. 

The bodies experience impulse of equal but opposite value during the collision due to which the velocity of the center of mass of the bodies after the collision are  
\begin{equation}
\vec{v_{af}} = \vec{v_{ai}}+\frac{j}{m_{a}}\vec{n} 
\end{equation}
\begin{equation}
\vec{v_{bf}} = \vec{v_{bi}}-\frac{j}{m_{b}}\vec{n}
\end{equation}

where $$\vec{v_{af}}$$ is the final velocity after collision, $$\vec{v_{ai}}$$ is the initial velocity before collision, $$m_{a}$$ is the mass of the body A and j is the impulse parameter.  

To simulate a simple collision of a rigid body to the ground, we allow the second rigid body to be the ground by assuming it is stationary $$(\vec{v_{bi}}=0)$$ and its mass infinite $$(m_{b}\rightarrow\infty)$$. Therefore, we only keep track of the velocity of the first body given by the equation (1a) and using the notion of impulse, its angular velocity after collision can be similarly determined, 
\begin{equation}
\omega_{af} = \omega_{ai}+\frac{\left(\vec{r}\times j\vec{n}\right)}{I_{a}}
\end{equation} 
where r is the distance vector from the center of mass of the rigid body to the collision point and $$I_{a}$$ is the moment of inertia of the body. 
Since the second rigid body is the ground, the impulse parameter j was simplified to be 
\begin{equation}
j=-\frac{(e+1) \vec{v_{\text{ap}}}\cdot \vec{n} }{\frac{\left(\vec{r}\times \vec{n}\right){}^2}{I_a}+\frac{1}{m_a}}
\end{equation}
where e is the elasticity of the collision, $$\vec{v_{\text{ap}}}$$ is the initial velocity of the impact point on the rigid body before collision. 
With
\begin{equation}
\vec{v_{\text{ap}}} = \vec{v_{ai}}+\omega_{ai}\times\vec{r}
\end{equation}
and the moment of inertia of the rigid body, 
\begin{equation}
I_{a} = \frac{m_{a}}{12}\left(w^2+h^2\right)
\end{equation}
and the direction perpendicular to the ground equal to,
\begin{equation}
\vec{n}=\hat{y}
\end{equation}
evaluating the impulse parameter j  
\begin{equation}
j=-\frac{\left(1+e\right)\left(v_{y}+\omega r_{x}\right)}{I_{a}+m_ar_{x}^2}I_{a}
\end{equation}
and the final expression of the vertical velocity of the center of mass of the body becomes 
\begin{equation}
V_{af}=v_{ai}-\frac{\left(1+e\right)\left(w^2+h^2\right)\left(v_{y}+\omega r_{x}\right)}{\left(w^2+h^2+12r_{x}^2\right)}
\end{equation}
and the angular velocity of the body is 
\begin{equation}
\omega_{af}=\omega_{ai}-\frac{12r_{x}\left(1+e\right)\left(v_{y}+\omega r_{x}\right)}{\left(w^2+h^2+12r_{x}^2\right)}
\end{equation}
Here $$v_{y}$$ is the vertical velocity component of $$v_{ai}$$.
Note there is no change introduced in the horizontal velocity component after collision since the impulse is only present in $$\hat{y}$$ and therefore is negligible in the simulation. 

## Coding the motion
Verlet integration method was used to model the motion of the rigid body in order to make it easier for adding new parameters and modifications. 
Here is the main code for calculating the  vertical position and the velocity of the rigid body's center of mass and its angular velocity at $$\delta t$$ and appending each to seperate lists. 
![code](https://github.com/nkhishig/nkhishig.github.io/blob/master/_posts/images/code2.jpg?raw=true)

We can plot each of them using the lists we created. Here is the vertical position, y vs time.  
![y](https://github.com/nkhishig/nkhishig.github.io/blob/master/_posts/images/y.jpg?raw=true)

Here is the velocity, $$v_{y}$$ vs time. 
![v](https://github.com/nkhishig/nkhishig.github.io/blob/master/_posts/images/v.jpg?raw=true)

Lastly, here is the plot of angular velocity $$\omega$$ vs time. 
![w](https://github.com/nkhishig/nkhishig.github.io/blob/master/_posts/images/omega.jpg?raw=true)

## Calculating energy and checking its conservation 
We have a solution, but is it correct? In order to check it's validity, we can determine whether or not the total energy of the system is conserved. 
The total energy is determined by
\begin{equation}
E_{total}=mgy+\frac{1}{2}mv^2+\frac{1}{2}I\omega^2
\end{equation}
where potential energy, kinetic energy and rotational kinetic energy contribute. 
Here is a plot that shows how each energy changes with time.  
![all](https://github.com/nkhishig/nkhishig.github.io/blob/master/_posts/images/all.jpg?raw=true)

And if we add them all up, we see that the total energy is conserved. 
![total](https://github.com/nkhishig/nkhishig.github.io/blob/master/_posts/images/totalE.jpg?raw=true)



