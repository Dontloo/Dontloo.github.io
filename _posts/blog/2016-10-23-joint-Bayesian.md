---
layout: post
title: "More on Joint Bayesian Verification"
modified:
categories: blog
excerpt:
tags: []
date: 2016-10-23
modified: 2016-10-23
---

### Derivations
The followings are some detailed derivatation of the formulars in the paper 
[Bayesian Face Revisited: A Joint Formulation](https://www.microsoft.com/en-us/research/publication/bayesian-face-revisited-a-joint-formulation/).  

**Eq.4 Background**  
\\[x=\mu+\epsilon\\]
where \\(\mu\\) and \\(\epsilon\\) follow two independent Gaussians \\(N(0,S_\mu)\\) and \\(N(0,S_\epsilon)\\).
The covariance matrices of \\(p(x_1,x_2|H_I)\\) and \\(p(x_1,x_2|H_E)\\) are given by
\\[\Sigma_I=\left[ \begin{matrix} 
  S_{\mu}+S_{\epsilon} & S_{\mu} \\\
  S_{\mu} & S_{\mu}+S_{\epsilon} \end{matrix} \right],\\]
\\[\Sigma_E=\left[ \begin{matrix} 
  S_{\mu}+S_{\epsilon} & 0 \\\
  0 & S_{\mu}+S_{\epsilon} \end{matrix} \right].\\]
  
**Eq.4**  
\\[r(x_1,x_2)=\log\frac{p(x_1,x_2|H_I)}{p(x_1,x_2|H_E)}=x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2+const,\\]
where
\\[A=(S_\mu+S_\epsilon)^{-1}-(F+G),\\]
\\[\left[ \begin{matrix} 
  F+G & G \\\
  G & F+G 
\end{matrix} \right]
=
\left[ \begin{matrix} 
  S_{\mu}+S_{\epsilon} & S_{\mu} \\\
  S_{\mu} & S_{\mu}+S_{\epsilon} 
\end{matrix} \right]^{-1}.\\]

**Derivation**  
\\[p(x_1,x_2|H_I)=\frac{1}{norm}exp(-\frac{1}{2}
\left[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \right] 
\Sigma_I^{-1}
\left[ \begin{matrix} 
  x_1 \\\ x_2
\end{matrix} \right]),\\]
where
\\[\left[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \right] 
\Sigma_I^{-1}
\left[ \begin{matrix} 
  x_1 \\\ x_2
\end{matrix} \right]
=
\left[ \begin{matrix} 
  x_1 & x_2
\end{matrix} \right] 
\left[ \begin{matrix} 
  F+G & G \\\
  G & F+G 
\end{matrix} \right]
\left[ \begin{matrix} 
  x_1 \\\ x_2
\end{matrix} \right]
=
x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2.\\]
\\[p(x_1,x_2|H_E)=\frac{1}{norm}exp(-\frac{1}{2}
\left[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \right] 
\Sigma_E^{-1}
\left[ \begin{matrix} 
  x_1 \\\ x_2
\end{matrix} \right]),\\]
where
\\[\left[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \right] 
\Sigma_E^{-1}
\left[ \begin{matrix} 
  x_1 \\\ x_2
\end{matrix} \right]
=
\left[ \begin{matrix} 
  x_1 & x_2
\end{matrix} \right] 
\left[ \begin{matrix} 
  (S_{\mu}+S_{\epsilon})^{-1} & 0 \\\
  0 & (S_{\mu}+S_{\epsilon})^{-1}
\end{matrix} \right]
\left[ \begin{matrix} 
  x_1 \\\ x_2
\end{matrix} \right]
=
x_1^T(S_{\mu}+S_{\epsilon})^{-1}x_1+x_2^T(S_{\mu}+S_{\epsilon})^{-1}x_2.\\]
\\[\therefore r(x_1,x_2)=\log\frac{p(x_1,x_2|H_I)}{p(x_1,x_2|H_E)}=x_1^T((S_\mu+S_\epsilon)^{-1}-(F+G))x_1+x_2^T((S_\mu+S_\epsilon)^{-1}-(F+G))x_2-2x_1^TGx_2+const=x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2+const\\]

**Eq.8 Background**  
\\[\mathbf{h}=[\mu;\epsilon_1;...;\epsilon_m]\\]
\\[\mathbf{x}=[x_1;...;x_m]\\]
\\[\mathbf{x}=P\mathbf{h}\\]
\\[P=\left[\begin{matrix}
I & I & 0 & \dots & 0 \\\
I & 0 & I & \dots & 0 \\\
\vdots & \vdots & \vdots & \ddots & \vdots \\\
I & 0 & 0 & ... & I
\end{matrix}\right]\\]
The distribution the hidden variable \\(\mathbf{h}\\) is \\(N(0,\Sigma_h)\\), where \\(\Sigma_h=diag(S_\mu,S_\epsilon,\dots,S_\epsilon)\\).

**Eq.8**  
\\[E(\mathbf{h}|\mathbf{x})=\Sigma_hP^T\Sigma_x^{-1}\mathbf{x}\\]

**Derivation**  
The distribution of \\(\mathbf{x}\\) is another Gaussian \\(N(0,\Sigma_x)\\)  where 
\\[\Sigma_x=P\Sigma_hP^T=\left[\begin{matrix}
S_{\mu}+S_{\epsilon} & S_{\mu} & \dots & S_{\mu} \\\
S_{\mu} & S_{\mu}+S_{\epsilon} & \dots & S_{\mu} \\\
\vdots & \vdots & \ddots & \vdots \\\
S_{\mu} & S_{\mu} & ... & S_{\mu}+S_{\epsilon}
\end{matrix}\right]\\]
ref: [Linear combinations of normal random variables](https://www.statlect.com/probability-distributions/normal-distribution-linear-combinations).  
More details can be found in [this question](https://www.zhihu.com/question/28086678) on zhihu.
<!---
\\[\mathbf{h}=P^\dagger\mathbf{x}=P^\dagger\Sigma_x\Sigma^{-1}_x\mathbf{x}=P^\dagger P\Sigma_hP^T\Sigma^{-1}_x\mathbf{x}=\Sigma_hP^T\Sigma^{-1}_x\mathbf{x}\\]
-->

### Discussion  
Why don't we just solve \\(\mathbf{h}=P^{\dagger}\mathbf{x}\\) directly instead of rewriting it in terms of \\(S_{\mu}\\) and \\(S_{\epsilon}\\)? 

Because it is not the only solution, since \\(\mathbf{h}\\) has one more degree of freedom than \\(\mathbf{x}\\). The scatter matrices of Linear Discriminant Analysis (LDA) mentioned in the paper can be thought of as another solution for \\(\mathbf{x}=P\mathbf{h}\\). This is sort of analogous to the biased variance estimation because we don't know where is the true mean \\(\mu\\).

So the paper has shown doing EM is a smarter choice.
