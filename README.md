# Construction of the FES and Identification of the Transition State

Using the R package **Metadynminer**, the **Free Energy Surface (FES)** can be estimated as a negative imprint of the added hills. Using the same package, the free energy minima and the transition path along with the transition state can be extracted for the system using the following equation:

$$
G_{(S)} = -kT \log(P(s)) = -\frac{(T+\Delta T)}{\Delta T} V(s) = -\frac{(T+\Delta T)}{\Delta T} \sum_i w_i \exp\left(-\frac{(s - S_i)^2}{2\sigma^2}\right)
$$

where:  

- \( G \) = free energy  
- \( V \) = metadynamics bias (flooding) potential  
- \( P \) = probability of a state with a collective variable \( s \)  
- \( k \) = Boltzmann constant  
- \( T \) = temperature in Kelvin  
- \( Delta T \) = an input parameter with the dimension of temperature (zero for unbiased simulation and infinity for the original metadynamics with constant hill heights)  
- \( w_i \) = height  
- \( S_i \) = position  
- \( sigma_i \) = width of each hill  

The first step is to use the slow but accurate `fes2` function to calculate the **FES**. This function explicitly evaluates the **Gaussian function** for every hill. The **FES** is calculated for **256×256 (2D) grid points**.  

The next step is to find the **free energy minima** using the function `minima`. The surface is divided by a **2D grid of 10 bins**, and minima are located for each bin. The **global minimum** refers to the most favored state of the system (i.e., the state with the highest probability).  

The **Nudged Elastic Band (NEB) method** is then used to construct the **transition path** between the minima of interest, allowing the **transition state**, defined as the point with the highest energy on this path, to be identified.
