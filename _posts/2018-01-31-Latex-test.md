\begin{equation}
\boldsymbol{\Omega}_{0}= \boldsymbol{Q}^{\textsf{T}}\dot{\boldsymbol{Q}}
\end{equation}

Rearranging gives 

\begin{equation}
\dot{\boldsymbol{Q}} = \boldsymbol{Q}\boldsymbol{\Omega}_{0}
\end{equation}
Differentiating $$\dot{\boldsymbol{Q}}$$,

\begin{equation}
\ddot{\boldsymbol{Q}} = \dot{\boldsymbol{Q}}\boldsymbol{\Omega}_{0} + \boldsymbol{Q}\dot{\boldsymbol{\Omega}}_{0} 
\end{equation}

\begin{equation}
\ddot{\boldsymbol{Q}} = \boldsymbol{Q}\boldsymbol{\Omega}_{0}^2 + \boldsymbol{Q}\dot{\boldsymbol{\Omega}}_{0} =\boldsymbol{Q}\left(\boldsymbol{\Omega}_{0}^2 + \dot{\boldsymbol{\Omega}}_{0} \right)
\end{equation}

\begin{equation}
\boldsymbol{Q}^{\textsf{T}}\ddot{\boldsymbol{Q}} = \boldsymbol{\Omega}_{0}^2 +\dot{\boldsymbol{\Omega}}_{0}
\end{equation}

equals

\begin{equation}
P = \boldsymbol{\Omega}_{0}^2 + \dot{\boldsymbol{\Omega}}_{0}
\end{equation}

We showed previously that
\begin{equation}
\textsf{sym}(P) = \boldsymbol{\Omega}_{0}^2
\end{equation}
so substituting that into Eq.5, we get
\begin{equation}
P=\textsf{sym}(P) +\dot{\boldsymbol{\Omega}}_{0}
\end{equation}

\begin{equation}
\dot{\boldsymbol{\Omega}}_{0} = P-\textsf{sym}(P) = P- \left(\frac{P+P^{\textsf{T}}}{2}\right) =  \left(\frac{P-P^{\textsf{T}}}{2}\right) = \textsf{skew}(P)
\end{equation}

where \textsf{skew}(P) is the skew-symmetric tensor of P. 
Now that 
\begin{equation}
\dot{\boldsymbol{\Omega}}_{0} = \textsf{skew}(P)
\end{equation}

Integrating both sides will result in
\begin{equation}
\boldsymbol{\Omega}_{0}\left(t\right)=\int_{z=0}^{t}\textsf{skew}(P)(z)dz, + \boldsymbol{\Omega}_{0}\left(0\right)
\end{equation}
