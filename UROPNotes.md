# UROP Notes 
### May 15, 2022: Meeting with Gaurav

Before the meeting, I read through some of the code in x-rayplay.ipynb, and added some comments of questions to discuss. Then Gaurav and I met. We first talked about the data file 
```
XRayData/scintillator-xray-data/gadox.txt
```
It has the format

| energy | linear attenuation |
| -------| -------------------|

where linear attenuation is the coefficient in $e^{-\alpha x}$. 

This is element wise substraction:
```
D = 50 # distance from metasurface to scintillator closest edge
T = 50 # thickness of scintillator (only T + Dreally matters for now)
depths = D + T .- scintillator_depths # vector of distance from 
```

Note to self - to print in Julia use 
```
println()
```
We then talked about this block
```
energy_indices = [25,34]
nE = 2
energies = energy[energy_indices]
decay_lengths = 1 ./ linatt[energy_indices] / (λ * 1e-9) # how many wavelengths are in this
frac = 0.9
```
Note to self - you can index into an array and create a new array by putting an array in the indexing bracket.

```
energies = energy[energy_indices]
```
We convert to amount of wavelengths 
```
decay_lengths = 1 ./ linatt[energy_indices] / (λ * 1e-9)
```
since these are the units we typically work in. Maxwell's equations are scale invariant (unlike quantum mechanics), and wavelength units are convenient. 
  
We talked about this line too:
```
println("Sensor-metasurface numerical aperture (NA): $(asin(gridL/(2F)))")
```
Let's talk about this: 
```
asin(gridL/(2F))
```

 + $\frac{1}{2} \cdot$ gridL is half the height of the (square) metasurface.
 + F is distance from source to metasurface
 Numerical aperature is $\theta$ formed by the right triangle. We can use inverse sine since we are using small angle approximation. 
 
We then talked about how to push to github. There are three things to do
```
git add -u
git commit
git push
```

Tips:
```
git diff --name-only
``` 
after you add, shows the files you changed
```
git diff --name-only --staged 
``` 
shows files staged (after add)