# Hardware-aware-Optimization-of-ECD-R-Sequence-Parameters
## Free Hamiltonian

$$ H = -\frac{\chi}{2}\hat{a}^\dagger \hat{a}\hat{\sigma}_z - \frac{\chi'}{2}\hat{a}^\dagger\hat{a}^\dagger\hat{a}\hat{a}\hat{\sigma}_z - K_s\hat{a}^\dagger\hat{a}^\dagger\hat{a}\hat{a} $$

Note that $\hat{n}^2 = \hat{n} + \hat{a}^\dagger\hat{a}^\dagger\hat{a}\hat{a}$ (i.e.,   $\hat{n}^2 \equiv\hat{a}^\dagger\hat{a}^\dagger\hat{a}\hat{a}$),  since the $\hat{n}$ term will be combined with the other Hamiltonian terms. Hence the Hamiltonian above describes 

$$ H \equiv \frac{\chi}{2}\hat{n}\hat{\sigma}_z - \frac{\chi'}{2}\hat{n}^2\hat{\sigma}_z- K_s\hat{n}^2$$ 

where $\chi$ is the first-order Dispersive shift, $\chi'$ is the second-order correction to the dispersive shift and $K_s$ is the Kerr self nonlinearity.


## Drive Hamiltonian
$$ H_d = C_I(t)[\hat{a}+ \hat{a}^\dagger] - i C_Q(t)[\hat{a}+ \hat{a}^\dagger] + q_I(t)\hat{\sigma}_x + q_Q(t)\hat{\sigma}_y$$

where $C_{I,Q}$ are the cavity drives in the $I-Q$ quadrature while $q_{I,Q}$ are the qubit drives in the $I-Q$ quadrature.

## Arbitrary unitary decomposition

Define the Echoed Conditional Displacement (ECD) gate as 

$$\text{ECD}(\beta) = D(\beta/2)|e\rangle |g\rangle + D(-\beta/2)|g\rangle |e\rangle = \sigma_xD(\beta\sigma_z/2)$$

where $\beta\in \mathbb{C}$ and $D(\alpha) = e^{\alpha \hat{a}^\dagger- \alpha^*\hat{a}}$.

Define arbitrary rotation as 

$$ 
R_\varphi(\theta) = \exp{\left[-i\frac{\theta}{2}(\sigma_x\cos(\varphi)+ \sigma_y\sin(\varphi))\right]} = \cos(\theta/2)I - i[\sigma_x\cos(\varphi)+ \sigma_y\sin(\varphi)]\sin(\theta/2).$$
 
where the right hand side is by the Euler identity since $[\sigma_x\cos(\varphi)+ \sigma_y\sin(\varphi)]^2=1$. i.e  Rotation by $\theta$ about the axis $(\cos\varphi, \sin\varphi, 0)$ in the $XY-$plane.

The ECD and Rotation gate form a universal gateset as seen in https://journals.aps.org/rmp/pdf/10.1103/RevModPhys.77.513

From above reference, the an ECD($\beta$) is decomposed into (hardware) gates (of 4 Displacements and one $\pi$ gate on the Transmon) such that 

$$\text{ECD}(\beta) \approx \text{ECD}(2i\alpha\sin(\chi T/2))$$

where $\chi$ is the dispersive coupling, $T$ is the total gate duration. Hence, the displacement in the cavity has a radius $\chi T \alpha$. Hence, from dimension analysis,  $\beta\sim \mu Hz $ since $\chi\sim KHz$, and $T \sim ns$. 

Recall that $\langle \beta |\hat{N}|\beta\rangle = \beta^2$, where $\hat{N} = \hat{a}^\dagger\hat{a}$. Hence, for the state $|\beta\rangle$ in the cavity the average number of photons is $|\beta|^2$ .i.e. If the number of photons feasible on a hardware is $\sim 30$, then the expected displacement distance is $\sim 5.477$.


The cost/fidelity function for gate ECD is defined as 

\[ \mathcal{F}= 1-\left|\frac{1}{\text{Tr}(P)}\text{Tr}(PU^\dagger_{\text{target}}U_{\text{ECD}})\right|^2\]

where $P$ is the projection unto the Hilbert space. $U_{ECD}$ is defined as follows

$$ U_{\text{ECD}} = D(\beta_{L+1})R_{\varphi_{L+1}}(\theta_{L+1})\cdot\text{ECD}(\beta_L)R_{\varphi_L}(\theta_L)\cdots \text{ECD}(\beta_1)R_{\varphi_1}(\theta_1).$$


Note the $P$ is the identity operator in this case since we want to consider the space of dimension $N_{\text{trunc}}$. 
