### Welcome to the analytical galactic chemical evolution model with terminal wind sampler!
How do Mg, Si, Ca, Ti, or so-called __&alpha;-elements__, evolve in dwarf galaxies? In this repository you will find the answer from a simple implementation of a one-zone Galactic Chemical Evolution model (GCE).

Although many analytical GCEs exist since the 1960s, here we introduce another unique solution: it combines gas inflow and forced gas outflow from a stellar system. 

The new model is called __Inflow with Ram Pressure Stripping (IRPS)__.

### Background

#### Abundances
To measure elemental abundances, it is typically to introduce the logarithmic value, which compares the ratio of the number of atoms of an element to the number of hydrogen atoms between the star in question and the Sun. In the case of iron, it is known as metallicity:

```math
\Biggl[\frac{Fe}{H}\Biggr]=log_{10}\Biggl[\frac{N_{Fe}}{N_H}\Biggr]_{star}-log_{10}\Biggl[\frac{N_{Fe}}{N_H}\Biggr]_{Sun}
```
Similarly, let's introduce  [&alpha;/H] for the sum of Mg, Si, Ca and Ti, and also the fraction  _Z_ __as the part of &alpha;-elements__ of some total mass:

```math
Z = Z_{Sun, \alpha} \cdot 10^{[\alpha/H]}
```
#### Mass conservation
What are processes and properties that affect the elemental evolution in the galactic scope? First, it is the mass conservation of gas _g_ and stars _s_:

```math
\frac{dg}{dt}=F-E-\frac{ds}{dt}
```

where _F_ and _E_ are gas inflow and gas outlflow, respectively, in the system. Dark matter is omitted in the chemical evolution and equations.

#### Star formation and galactic gas loss
The most massive stars live the shortest lives: their core-collapse deaths are responsible for &alpha;-elements' main contribution. Taking into account elements produced from only these supernovae allows to use the so-called _instantaneous recycling approximation_.
From this, we need to make a guess about the term ds/dt (s = &lambda; S, for surviving stars only; S - total mass of ever born stars), which we recall here from star formation history &psi; from Kennicutt-Schmidt law (1953) (&psi; ~ g):

```math
\frac{ds}{dt}=(1-R) \psi =\lambda \psi =\beta g
```
where &lambda; - locked-in-stars mass, _R_ - _return fraction_ of already dead stars, &beta; - star formation efficiency (efficiency of how effectively gas can be transformed into stars). Because star formation includes birth of massive stars too, the gas outflow from the system should be proportional with a mass-loading factor &eta; to star formation as well:

```math
E = \eta \beta g + E'_s
```
where the second term is a constant which will be included only after some moment in time. That moment we associate with &alpha;-abundance of the gas in the stellar system equal to [&alpha;/H]<sub>s</sub>. 
In the final equations, we use the substitutions &xi; = F/(&beta;(1+&eta;)) and &zeta; = E'<sub>s</sub>/(&beta;(1+&eta;)). 

#### Metal-fraction equation
Finally, for &alpha;-abundance injection/loss we have:

```math
\frac{dgZ}{dt} = q \psi + RZ \psi - Z \psi -Z_E E + Z_F F
```
where q - yield of elements in question, Z<sub>E</sub>, Z<sub>F</sub> - loss and contribution of &alpha;-elements from the systemic gas loss and inflow, respectively. Let's also introduce the _effective yield_:

```math
p_{eff} = \frac{p}{1+\eta} = \frac{q}{\lambda(1+\eta)}
```

### What this repository is about?

This repository contains a Jupyter Notebook that allows the user to build the analytical solution to the above equations:

```math
\frac{ds}{dZ} = f(Z)
```
```math
Z = Z_1(g)~~~~([\alpha/H]<[\alpha/H]_s)
```
```math
Z = Z_2(g)~~~~([\alpha/H]>[\alpha/H]_s)
```
where the first function (&alpha;-elements distribution function (ADF) among the observed stars in the small galaxy) takes into account gas metallicity, which must be found from the equations above. There are two equations _Z=Z(g)_, before and after [&alpha;/H]<sub>s</sub> (the alpha abundance at which ram pressure stripping occured). 


### How to use it?

The rest of the notebook gives examples on how to use the equations. 
The &alpha;-distribution function can be compared to the observed histogram of &alpha;-abundances of stars from some given galaxy to find the best-fitting parameters: effective yield, &zeta;/&xi;, ram pressure stripping metallicity. 

For questions, contact kkvasova@nd.edu.


