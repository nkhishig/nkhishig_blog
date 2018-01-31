\begin{equation}
\Omega_{0}= Q^{T}\dot{Q}
\end{equation}
Rearranging gives 
\begin{equation}
\dot{Q} = Q\Omega_{0}
\end{equation}
Differentiating $$\dot{Q}$$,
\begin{equation}
\ddot{Q} = \dot{Q}\Omega_{0} + Q\dot{\Omega}_{0} 
\end{equation}
\begin{equation}
\ddot{Q} = Q\Omega_{0}^2 + Q\dot{\Omega_{0}} =Q\left(\Omega_{0}^2 + \dot{\Omega}_{0} \right)
\end{equation}
\begin{equation}
Q^{T}\ddot{Q} = \Omega_{0}^2 +\dot{\Omega}_{0}  \rightarrow
P =  \Omega_{0}^2 + \dot{\Omega}_{0} 
\end{equation}
We showed previously that
\begin{equation}
Sym(P) = \Omega_{0}^2
\end{equation}
so substituting that into Eq.5, we get
\begin{equation}
P=Sym(P) +\dot{\Omega}_{0}
\end{equation}
\begin{equation}
\dot{\Omega}_{0} = P-Sym(P) = P- \left(\frac{P+P^{T}}{2}\right) =  \left(\frac{P-P^{T}}{2}\right) = Skew(P)
\end{equation}
where Skew(P) is the skew-symmetric tensor of P. 
Now that 
\begin{equation}
\dot{\Omega}_{0} = Skew(P)
\end{equation}
Integrating both sides will result in
\begin{equation}
\Omega_{0}\left(t\right)=\int_{z=0}^{t}Skew(P)(z)dz + \Omega_{0}\left(0\right)
\end{equation}
