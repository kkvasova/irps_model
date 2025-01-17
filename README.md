### Welcome to analytical galactic chemical evolution model with terminal wind sampler!
How are Mg, Si, Ca, Ti, or so-called __&alpha;-elements__, evolved in dwarf galaxies? In this repository you find the answer from simple implementation of what is called one-zone Galactic Chemical Evolution model (GCE).

Despite many of analytical GCE exist since 1960s, here we introduce the unique solution: it combines gas inflow and the forced gas outflow from the stellar system. 

The new model is called __Inflow with Ram Pressure Stripping (IRPS)__.

### Background

#### Abundances
To measure elemental abundances in stars and not only, it is typically to introduce the logarithmic value which compares the number of elements to the number of hydrogen atoms between the star in question and the Sun. In the case of iron, it is known as metallicity:

```math
\Biggl[\frac{Fe}{H}\Biggr]=log_{10}\Biggl[\frac{N_{Fe}}{N_H}\Biggr]_{star}-log_{10}\Biggl[\frac{N_{Fe}}{N_H}\Biggr]_{Sun}
```
Similarly, let's introduce  [&alpha;/H] for the sum of Mg, Si, Ca and Ti, and also the fraction of unit  _Z_ __as the part of &alpha;-elements__ of some total mass:

```math
Z = Z_{Sun, \alpha} \cdot 10^{[\alpha/H]}
```
#### Mass conservation
What are the processes and properties which affect the elemental evolution in the galactic scope? First, it is gas _g_ and stars _s_ total mass conservation:

```math
\frac{dg}{dt}=F-E-\frac{ds}{dt}
```

where _F_, _E_ - gas inflow and gas outlflow in the system. Dark matter is omitted in the chemical evolution and equations as well.

#### Star formation and galactic gas loss
The heaviest stars live the shortest lives: their core-collapse deaths are responsible for &alpha;-elements main contribution. Taking into account elements produced from only this process allows to use so called _instantaneous recycling approximation_.
From this, as we need to make a guess about the term ds/dt (s = &lambda; S, for still existing stars only; S - total mass of ever born stars), which we recall here from star formation history, &psi; ~ g, from Kennicutt-Schmidt law (1953):

```math
\frac{ds}{dt}=(1-R) \psi =\lambda \psi =\beta g
```
where &lambda; - locked-in-stars mass, _R_ - fraction of already dead stars, &beta; - star formation efficiency (efficiency of how effectively gas can be transformed into stars). As star formation includes birth of massive stars too, the gas outflow from the system should be proportional with mass-loading factor &eta; to star formation as well:

```math
E = \eta \beta g + E'_s
```
where the second term is a constant which will be included only after some moment in time. That moment we associate with &alpha;-abundance of the gas in the stellar system equal to [&alpha;/H]<sub>s</sub>. 
In final equations, we use terms &xi; = F/(&beta;(1+&eta;)) and &zeta; = E'<sub>s</sub>/(&beta;(1+&eta;)). 

#### Metal-fraction equation
Finally, for &alpha;-abundance injection/loss we have:

```math
\frac{dgZ}{dt} = q \psi + RZ \psi - Z \psi -Z_E E + Z_F F
```
where q - the yield of elements in question from stellar deaths, Z<sub>E</sub>, Z<sub>F</sub> - loss and contribution of &alpha;-elements from the systemic gas loss and inflow respectively. Let's also introduce effective yield:

```math
p_{eff} = \frac{p}{1+\eta} = \frac{q}{\lambda(1+\eta)}
```

### What this repository is about?

This repository contains the Jupyter-Notebook, which allows the user to build the solution of the analytical solution of the above equations:

```math
\frac{ds}{dZ} = f(Z);
```
```math
Z = Z_1(g)~~~~([\alpha/H]<[\alpha/H]_s);
```
```math
Z = Z_2(g)~~~~([\alpha/H]>[\alpha/H]_s)
```
where the first function (&alpha;-elements distribution fucntion (ADF) among the observed stars in the small galaxy) takes into account the gas, which must be found from the equations below. There are two equations _Z=Z(g)_, before and after [&alpha;/H]<sub>s</sub> (the ram pressure stripping occured). 

All functions are implemented in the repository, but they are way too long.

### What it contains and how to use it?

After you upload the Jupyter-Notebook, in your access will be functions with next arguments:

| Function         | Input                                                                                        | Output                                                       |
|------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| eq_before_g      | F - inflow in &xi;                                                                           |    Returns &alpha;-abundances as                             |
|                  | z<sub>inflow</sub> =  Z<sub>F</sub>/p<sub>eff</sub>                                          | the function of input array                                  |
|                  | z<sub>initial</sub> = Z<sub>0</sub>/p<sub>eff</sub> - initial gas cloud &alpha;-abundance    | from the function Z = Z<sub>1</sub>(g)                       |
|                  | g - gas, an array                                                                            |  (before ram pressure stripping).                            |
|                  | g<sub>in</sub> - initial fraction of gas mass from the stellar system, in initial mass units it's 1 |                                                              |
| g_rps            | F - inflow in &xi;                                                                           |  Returns the value of gas                                    |
|                  | z<sub>inflow</sub> =  Z<sub>F</sub>/p<sub>eff</sub>                                          | when [&alpha;/H]=[&alpha;/H]<sub>stripped</sub>              |
|                  | z<sub>initial</sub> = Z<sub>0</sub>/p<sub>eff</sub>                                          |                                                              |
|                  | z<sub>str</sub> = Z<sub>stripped</sub>/p<sub>eff</sub>                                       |                                                              |
| long_coef        | F - inflow in &xi;                                                                           | The equation   Z = Z<sub>2</sub>(g)                          |
|                  | Es - outflow in &zeta;                                                                       | contains a long constant for                                 |
|                  | z<sub>inflow</sub> =  Z<sub>F</sub>/p<sub>eff</sub>                                          | all values of gas                                            |
|                  | z<sub>initial</sub> = Z<sub>0</sub>/p<sub>eff</sub>                                          | (&alpha;-abundances) term,                                   |
|                  | g<sub>in</sub> - initial fraction of gas mass from the stellar system, in initial mass units it's 1    | which we placed outside                                      |
| eq_after_g_abs   | F - inflow in &xi;                                                                           |    Returns &alpha;-abundances as                             |
|                  | Es - outflow in &zeta;                                                                       | the function of an input array                               |
|                  | z<sub>inflow</sub> =  Z<sub>F</sub>/p<sub>eff</sub>                                          | from the function Z = Z<sub>2</sub>(g)                       |
|                  | z<sub>initial</sub> = Z<sub>0</sub>/p<sub>eff</sub>                                          |   (after ram pressure stripping).                            |
|                  | long_coef - the supplemental long constant value,                                            |                                                              |
|                  | measured in the external function                                                            |                                                              |
|                  | g - gas, an array                                                                            |                                                              |
|                  | g<sub>in</sub> - initial fraction of gas mass from the stellar system, in initial mass units it's 1    |                                                              |
| eq_after_g_equal | F - inflow in &xi;                                                                           | Similar to _eq_after_g_abs_                                  |
|                  | z<sub>inflow</sub> =  Z<sub>F</sub>/p<sub>eff</sub>                                          | but in the case &xi;=&zeta;                                  |
|                  | z<sub>initial</sub> = Z<sub>0</sub>/p<sub>eff</sub>                                          |                                                              |
|                  | g - gas, an array                                                                            |                                                              |
|                  | g_in - initial fraction of gas mass from the stellar system, in initial mass units it's 1    |                                                              |
| gas_equation     | p<sub>eff</sub> - the effective yield,                                                       | Compiles _eq_after_g_abs_                                    |
|                  | F - inflow in &xi;                                                                           | and _eq_before_g_abs_                                        |
|                  | Es - outflow in &zeta;                                                                       | and returns gas values                                       |
|                  |  aH<sub>inflow</sub> = [&alpha;/H]<sub>F</sub>                                               | for designated array of                                      |
|                  |  aH<sub>initial</sub> = [&alpha;/H]<sub>0</sub>                                              | [&alpha;/H] values                                           |
|                  |  aH<sub>str</sub> = [&alpha;/H]<sub>s</sub>,                                                 |                                                              |
|                  | points = 5001, (amount of points in the array of                                             |                                                              |
|                  | ds/dZ~ds/d[&alpha;/H]))                                                                      |                                                              |
|                  | show=True - whether to show or not to show the g([&alpha;/H]) figure                         |                                                              |
| a2               | p - the effective yield,                                                                     |                                                              |
|                  | aH<sub>f</sub> = [&alpha;/H]<sub>F</sub>,                                                    | Returns ds/d[&alpha;/H] values                               |
|                  | F - inflow in &xi;                                                                           | for specified parameters:                                    |
|                  | E - outflow in &zeta;                                                                        | p<sub>eff</sub>, &zeta;/&xi;                                 |
|                  | alphah - array of equally spaced [&alpha;/H] points,                                         | (with &xi; fixed as                                          |
|                  | gas - gas, an array of points predetermined for [&alpha;/H] array in aH array,               | 10 before and 0.01 after intense gas loss                    |
|                  | aH<sub>str</sub>=[&alpha;/H]<sub>s</sub>                                                     |    [&alpha;/H]<sub>F</sub>                                   |
|                  | show=False - whether to show or not to show supplemental g(&alpha;/H) and other plots        |  and array of [&alpha;/H]                                    |
|                                                                                                                                                                                |

The function _a2_ takes as input three main parameters: the structure of the equations is so, that &xi; can be a normalization factor. The gas values for each &alpha;-abundance array is predetermined in function _gas_equation_, which combines equations before ram pressure stripping occurs and after. 

### How to use it?

The rest of Jupyter-Notebook is referred to some proposed examples on how to use the functions. 
In prospective, the &alpha;-distribution function can be compared to the observed histogram of &alpha;-abundances of stars from some given galaxy to find the best-fitting parameters: effective yield, &zeta;/&xi;, inflow metallicity. 

For questions, contact kkvasova@nd.edu.


