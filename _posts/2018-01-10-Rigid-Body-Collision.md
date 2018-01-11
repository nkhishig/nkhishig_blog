
## Rigid Body Collision Theory  

For two rigid bodies in collision the equations of motion are determined using the concept of impulse. We make the assumption that the collision happens quickly enough that there is no change in the position or orientation of the bodies. Also we do not account for friction when computing the forces in the system, allowing only the force in the direction perpendicular to the edge of the bodies during the collision, noted by the unit vector $$\vec{n}$$. 

The bodies experience impulse of equal but opposite value during the collision due to which the velocity of the center of mass of the bodies after the collision are  
\begin{equation}
\vec{V_{af}} = \vec{V_{ai}}+\frac{j}{m_{a}}\vec{n} 
\end{equation}
\begin{equation}
\vec{V_{bf}} = \vec{V_{bi}}-\frac{j}{m_{b}}\vec{n}
\end{equation}

where $$\vec{V_{af}}$$ is the final velocity after collision, $$\vec{V_{ai}}$$ is the initial velocity before collision, $$m_{a}$$ is the mass of the body A and j is the impulse parameter.  

To simulate a simple collision of a rigid body to the ground, we allow the second rigid body to be the ground by assuming it is stationary $$(\vec{V_{bi}}=0)$$ and its mass infinite $$(m_{b}\rightarrow\infty)$$. Therefore, we only keep track of the velocity of the first body given by the equation (1a) and using the notion of impulse, its angular velocity after collision can be similarly determined, 
\begin{equation}
\omega_{af} = \omega_{ai}+\frac{\left(\vec{r}\times j\vec{n}\right)}{I_{a}}
\end{equation} 
where r is the distance vector from the center of mass of the rigid body to the collision point and $$I_{a}$$ is the moment of inertia of the body. 
Since the second rigid body is the ground, the impulse parameter j was simplified to be 
\begin{equation}
j=-\frac{(e+1) \vec{V_{\text{ap}}}\cdot \vec{n} }{\frac{\left(\vec{r}\times \vec{n}\right){}^2}{I_a}+\frac{1}{m_a}}
\end{equation}
where e is the elasticity of the collision, $$\vec{V_{\text{ap}}}$$ is the initial velocity of the impact point on the rigid body before collision. 
With
\begin{equation}
\vec{V_{\text{ap}}} = \vec{V_{ai}}+\omega_{ai}\times\vec{r}
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
j=-\frac{\left(1+e\right)\left(V_{y}+\omega r_{x}\right)}{I_{a}+m_ar_{x}^2}I_{a}
\end{equation}
and the final expression of the vertical velocity of the center of mass of the body becomes 
\begin{equation}
V_{af}=V_{ai}-\frac{\left(1+e\right)\left(w^2+h^2\right)\left(V_{y}+\omega r_{x}\right)}{\left(w^2+h^2+12r_{x}^2\right)}
\end{equation}
and the angular velocity of the body is 
\begin{equation}
\omega_{af}=\omega_{ai}-\frac{12r_{x}\left(1+e\right)\left(V_{y}+\omega r_{x}\right)}{\left(w^2+h^2+12r_{x}^2\right)}
\end{equation}
Here $$V_{y}$$ is the vertical velocity component of $$V_{ai}$$.
Note there is no change introduced in the horizontal velocity component after collision since the impulse is only present in $$\hat{y}$$ and therefore is negligible in the simulation. 

## Coding the motion
Verlet integration method was used to model the motion of the rigid body in order to make it easier for adding new parameters and modifications. 

\text{Module}\left[\left\{a=2,b=2,\text{yi}=10,\text{vi}=0,\text{$\delta $t}=0.01,\text{$\theta $i}=\frac{30 \pi }{180},e=1\right\},\omega _1=0;\omega _2=0;y_1=\text{yi};v_1=\text{vi};v_2=0;\theta _1=\text{$\theta $i};\text{For}\left[t=0,t<10,t\text{+=}\text{$\delta $t},\left\{\text{AppendTo}\left[\text{list2},y_1\right],\text{AppendTo}\left[\text{list3},\theta _1\right],\text{AppendTo}\left[\text{list4},\omega _1\right],\text{AppendTo}\left[\text{list5},v_1\right],\theta _1=\text{$\delta $t} \omega _1+\theta _1,y_1=-4.9 \text{$\delta $t}^2+\text{$\delta $t} v_1+y_1,v_1=v_1-9.8 \text{$\delta $t},y_2=-4.9 \text{$\delta $t}^2+\text{$\delta $t} v_1+y_1,\text{If}\left[r_y\left(n\left(\theta _1\right),\theta _1\right)+y_2<0,\left\{y_1=-r_y\left(n\left(\theta _1\right),\theta _1\right),\omega _2=\omega _1-\frac{12\ 2 r_x\left(n\left(\theta _1\right),\theta _1\right) \left(\omega _1 r_x\left(n\left(\theta _1\right),\theta _1\right)+v_1\right)}{12 r_x\left(n\left(\theta _1\right),\theta _1\right){}^2+a^2+b^2},v_2=v_1-\frac{2 \left(a^2+b^2\right) \left(\omega _1 r_x\left(n\left(\theta _1\right),\theta _1\right)+v_1\right)}{12 r_x\left(n\left(\theta _1\right),\theta _1\right){}^2+a^2+b^2},\omega _1=\omega _2,v_1=v_2\right\}\right]\right\}\right]\right]

## Calculating energy and checking its conservation 



