<center><font face="font" size=6>CS3226 Notes</font></center>
</br>  
<center><a href="https://yzhanglp.com" title="personal website">ZHANG Yuhao</a></center>

# Lecture 1 Measure
Link to [Lecture Notes 1](../materials/01-Measures.pdf)
## Definition & Property
- To measure the information quantity of a event, we should define a measure to measure the information quantity we get if a event happened.
- Generically speaking, if A occurs with probability p, then we define:
  $$Information(A)=\psi(p)$$

<details> <summary>Intuition</summary>
 The intuition that we use <b>p</b> to measure the Information is can be understand as the happen of A change a random event A to a determinstic result. Thus the information quantity should be related with <b>p</b> 
 </details>
Some natural properties that a mesure $\psi(p)$ should have:  

1. (Non-negativity), $\psi(p)>0$ i.e, we can not learn a negative amount of inforamtion
2. (Zero for definite event), $\psi(1)=0$
3. (Monotonicity), If $p\leq{p^{'}}$ then $\psi(p)\ge{\psi{p^{'}}}$
4. (Continuity) $\psi(p)$ is continous in p
5. (Additivity under Independence) $\psi(p_{1}p_{2}) = \psi(p_1)+\psi(p_2)$ if A and B are independent event happened with probability $p_1$ and $p_2$

 - It can be shown that $\psi(P)=\log_{b}\frac{1}{p}$ can satisfied the property we want a information measure can have.
 - We focus on b=2. Which means the information is measured in "bits".
  
 ## Information of Random Varible - Entropy
 ### Definition
 - Let $X$ be a discrete random varible with probability mass function $P_X$
 - We define (Shannon) entropy as the Following:    
 $$\begin{align*}
 H(X) &= E_{X{\sim}x}[\log_{2}\frac{1}{P_{X}(X)}] \\
 &= \sum_{x}P_{X}(x)log_{2}\frac{1}{P_{X}(x)}
\end{align*}$$
- Intuition: The happen of a event **x** with probability $P(x)$ will give us a information quantity $log_{2}\frac{1}{P(x)}$, thus to define the information of a Random Varible, it is reasonable to use the expection of information gained.
**Examples:**
- Binary source:
 Suppose $X\sim{Bernoulli(p)}$ for some $p\in{(0,1)}$
 Then use the defined entropy, we have:
 $$H(X) = p \log_{2}\frac{1}{p}+(1-p)\log_{2}\frac{1}{1-p}$$

 - We can show that the entropy will have a max value at $p=\frac{1}{2}$
 - Can generlize to uniform distribution random varible.$H(X) = \log{(\left |M\right |)}$ with all event happened in probability $\frac{1}{\left |M\right |}$ (Also largest entropy with M events)
  
### Variations
**Joint entropy of two random varibles $(X,Y)$**: 
 $$\begin{align*}
 H(X,Y) &= E_{(X,Y){\sim}P_{XY}}[\log_{2}\frac{1}{P_{XY}(X,Y)}] \\
 &= \sum_{x,y}P_{XY}(x,y)log_{2}\frac{1}{P_{XY}(x,y)}
 \end{align*}$$
- Intuition:Just treat $(X,Y)$ as a RV and use the definition

**Condition entropy of Y given X:**
 $$\begin{align*} H(X|Y) &=E_{(X,Y){\sim}P_{XY}}[\log_{2}\frac{1}{P_{Y|X}}(Y|X)]\\
  & = \sum_{x,y}P_{XY}(x,y)log_{2}\frac{1}{P_{Y|X}{(y|x)}}\\
  & = \sum_{x}P_{X}(x)H(Y|X=x)
  \end{align*}$$

- In the last term, $H(Y|X=x)=\sum_{y}P_{Y|X}(y|x)\log_{2}\frac{1}{P_{Y|X}(y|x)}$.
- Intuition: Noticed that $H(Y|X=x)$ is the entropy of Y given a certain X. The Conditional Entropy only do averge on all the $X\sim{x}$. Thus the Conditional Entropy represent the uncertainty of $Y$ after observing $X$. 

## Property of Entropy
- **Non-negativity:** $$H(X)\ge{0}$$

- **Upper bound:** If $X$ takes values on a finite alphabet $\chi$, then:
 $$H(X)\leq{log_2{\chi}}$$
  Intuition: The uniform distribution has most uncertainty
  Proof: to be add
  Intuition of proof: Use a unform distributed $Q$

- **Chain rule:**
 $$H(X,Y)=H(X)+H(Y|X)$$
  Intuition: The overall information $(X,Y)$ is the information in X plus the remaining information in Y after observeing X.
Proof: to be add.

- **Chain rule:(general):**
 $$H(X_{1},...,X_{n})=\sum_{i=1}^{n}H(X_{i}|X_1,...,X_{i-1})$$
Proof: Use the expansion: 
 $$P_{X_1,...,X_n} = P_{X_1}\times{P_{X_2|X_1}}\times{P_{X_3|X_1,X_2}}\times...\times{P_{X_{n}|X_1,...,X_{n-1}}}$$
- **Sub-additivity:**
 $$H(X_1,...X_n)\leq{\sum_{i=1}^{n}H(X_i)}$$

## KL Divergence  
### Definition:  
 $$\begin{align*}
D(P||Q) &= \sum_{x}P(x)log_{2}\frac{P(X)}{Q(X)}\\
&=E_{X\sim{P}}[log_{2}\frac{P(X)}{Q(X)}]
\end{align*}$$
- Can be viewed as a kind of "distance" measure the Difference between P and Q, but not a distance function in mathematical sense.  
- We can show $D(P||Q)$ always larger than 0 by use $\log{x}\leq{x-1}$  

## Mutual Information
### Definition
- Mutual information:
  $$I(X;Y)=H(Y)-H(X|Y)$$
- Intuition:  
  H(Y) is prior uncertainty in Y, H(Y|X) is the remaining uncertainty after observing X. Thus I(X;Y) is the amount about Y **We Learn** by **observing** X (on averge). Which stands for Mutual information between Y and X.  
### Properties of Mutual Information  
- Alternative forms:  
$$\begin{align*}
I(X;Y) &= D(P_{XY}||P_{X}\times{P_{Y}})\\
&=E\left[log_{2}\frac{P_{XY}(X,Y)}{P_X(X)P_Y(Y)}\right ]\\
&=E\left [log_{2}\frac{P_{Y|X}(Y|X)}{P_Y(Y)}\right ]\\
&=\sum{x,y}P_{XY}(x,y)log_2\frac{P_{Y|X}(x,y)}{P_Y(y)}
\end{align*}$$
- Proof: just substitute $H(Y)$ and $H(Y|X)$ with the difintion of entropy  
- Symmetry: We have:  
$$ I(X;Y) = H(X)+H(Y)-H(X,Y) = I(Y;X)$$
- Non-negativity
- Upper bounds:
  $$I(X;Y)\leq{H(X)}\leq{log_2|\chi|}$$
  $$I(Y;X)\leq{H(Y)}\leq{log_2|\mathbb{Y}|}$$
- Chain rule: Similar with Entropy term
- Sub-additivity Similar with Entropy
- Data processing inequality:  
  Given X and Z are conditionally independent given Y then:
  $$I(X;Z)\leq{I(X;Y)}$$
- Intuition Processing Y to produce Z can not increase the information available regarding X.
- Proof: Use $P_{Z|XY}=P_{Z|Y}$ and $H(X)-H(X|Z)\leq{H(X)-H(X|Y,z)}$

## Conclusion  
- The lecture 1 mainly give some basic difinition of information theory. Like Entropy, KL-Divergence, Mutual Information, they share some similar property and all use to measure the information quantity(uncertainty), the proof follows simply use the defintion and some basic equation.