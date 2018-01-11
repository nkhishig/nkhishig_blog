
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

```Mathematica
Module[{a = 2, b = 2, yi = 10, 
  vi = 0, \[Delta]t = 0.01, \[Theta]i = 30/180 \[Pi], e = 1},
 Subscript[\[Omega], 1] = 0;
 Subscript[\[Omega], 2] = 0;
 Subscript[y, 1] = yi;
 Subscript[v, 1] = vi;
 Subscript[v, 2] = 0;
 Subscript[\[Theta], 1] = \[Theta]i;
 For[t = 0, t < 10, t += \[Delta]t,
  {AppendTo[list2, Subscript[y, 1]], 
   AppendTo[list3, Subscript[\[Theta], 1]], 
   AppendTo[list4, Subscript[\[Omega], 1]], 
   AppendTo[list5, Subscript[v, 1]],
   Subscript[\[Theta], 1] = 
    Subscript[\[Theta], 1] + Subscript[\[Omega], 1] \[Delta]t,
   Subscript[y, 1] = 
    Subscript[y, 1] + Subscript[v, 1] \[Delta]t - 4.9 \[Delta]t^2,
   Subscript[v, 1] = Subscript[v, 1] - 9.8 \[Delta]t,
   Subscript[y, 2] = 
    Subscript[y, 1] + Subscript[v, 1] \[Delta]t - 4.9 \[Delta]t^2,
   If[Subscript[y, 2] + 
      Subscript[r, y][n[Subscript[\[Theta], 1]], Subscript[\[Theta], 
       1]] < 0, 
    {Subscript[y, 
      1] == -Subscript[r, y][n[Subscript[\[Theta], 1]], 
        Subscript[\[Theta], 1]],
     Subscript[\[Omega], 2] = 
      Subscript[\[Omega], 1] - 
       12 Subscript[r, x][n[Subscript[\[Theta], 1]], 
         Subscript[\[Theta], 
         1]] (2) (Subscript[v, 1] + 
           Subscript[\[Omega], 1]*
            Subscript[r, x][n[Subscript[\[Theta], 1]], 
             Subscript[\[Theta], 1]])/(a^2 + b^2 + 
           12 (Subscript[r, x][n[Subscript[\[Theta], 1]], 
              Subscript[\[Theta], 1]])^2),
     Subscript[v, 2] = 
      Subscript[v, 
       1] - ((a^2 + b^2) (2) (Subscript[v, 1] + 
            Subscript[\[Omega], 1]*
             Subscript[r, x][n[Subscript[\[Theta], 1]], 
              Subscript[\[Theta], 1]]))/(a^2 + b^2 + 
          12 (Subscript[r, x][n[Subscript[\[Theta], 1]], 
             Subscript[\[Theta], 1]])^2),
     Subscript[\[Omega], 1] = Subscript[\[Omega], 2],
     Subscript[v, 1] = Subscript[v, 2]
     }]}]]
```

## Calculating energy and checking its conservation 



