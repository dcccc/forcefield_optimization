
A python code used to optimize gaff type forcefield with dataset. The single molecula, dimer or pbc structure system are supported.


# Theory

To optimize forcefield parameters, generally speaking, the loss function can be expressed as 

$$ f(x) = a*\Delta C + b*\Delta E + c*\Delta F  + d*\Delta H \cdots $$

Here,  
$x$ is the forcefield paramters  
$\Delta C$ is the coordinate differences  
$\Delta E$ is the energy differences  
$\Delta F$ is the force differences    
$\Delta F$ is the hessian differences  
and so on  
Those differences may be not a plain and direct value differences between the values calculated by forcefield and the refercence values in dataset.  

a,b,c,d and so on are the weight of those terms. They can be determined with some sophisticated method related to the value differences or distributions differences between values calculated by forcefield and the refercence values in dataset.

There are several usual circustances as below:  
1. only data of energy and coordinate in dataset  
  The weigth a and b are valid, and other weights are zeros. As the coordinates are not changed during forcefield optimization, the value of $\Delta C$ is zero. Only energy differences related items remains  
  The dataset may be a simple of md simualtion trajectory. If so, the energy distribution difference is of much importance when free energy of the system are our purpose. Because the free energy of the systems are the same if the energy distributions are identical.  
  
2. data of force, energy and coordinate in dataset  
  Weight b and c are valid.    
  
3. data of energy and coordinate in dataset, and the stuctures are optimized  
  The fact of optimized stuctures indciates the zeros forces on atoms. Although the weight c may be still zeros. The energy by forcefield can also be the enegies of the optimized structures. Then the forces are included in the loss functions with a implicit way. And the $\Delta C$ can be used to evaluate the accuracy of the optimized forcefield, if a is setted to zeros.


# Forcefield_optimization

Here only the deriatives of energy to the forcefield parameters are calculated in the above jupyter notebooks. The the calculation of deriatives of forces to the forcefield parameters is very complex, and the calculation require much more memory and cpu hour than the deriatives of energy. So the present function is limited. But it is a nice trial to optimize forcefields with it, and get beter forcefields with large chance, compared with the general forcefield.  

About the detial of the forcefield optimizing, please refer to the jupyter notebooks.

# Problem  
1. As there is no available appropriate dimer and pbc structure datasets, the forcefield optimizing of dimer and pbc structure system are not tested. there maybe bugs in it.  
2. Only single component sysytems are supported.  
3. If you have a dataset of single molecules, dimers and pbc structure mixtures and you want to optimize forcefield paramters with those data all at same time, then you have to calculate the ff_items of the three kind of data seperately and stack them together as one dataset. The data format of ff_items is same for single molecules, dimers and pbc structures. You can refer to the code for more details.

# To do  
1. The structures optimizing during the forcefield paramter optimizing(circustances 3)




