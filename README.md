# Cell Quality Remediation Module
This module was developed by [ATA Engineering](http://www.ata-e.com) as an 
add-on to the Loci/CHEM computational fluid dynamics (CFD) solver. The module 
is useful for obtaining a solution on poor quality meshes. 

As part of 
the flux calculation for each cell face in the mesh, solution values 
at cell faces must be reconstructed from solution values at cell 
centers (since Loci/CHEM is a cell centered finite volume code). To 
achieve second order spatial accuracy a first order reconstruction 
is used. However, Loci/CHEM will by default use a more robust, but 
less accurate, zeroth order reconstruction in regions of poor cell 
quality. This zeroth order reconstruction results in locally first order
spatial accuracy. Loci/CHEM determines that cells with a volume ratio 
greater than 50, or a maximum included angle of greater than 150 degrees
constitute poor quality regions. If the region of poor cell quality is small, this local change can have a negligible effect on solution accuracy, while greatly helping robustness.

This module extends the functionality in Loci/CHEM by allowing the 
user to decrease the volume ratio and maximum included angle thresholds
from their default values. It also allows the user to include of all 
cells adjacent to those flagged by the volume ratio and maximum angle 
thresholds in the poor quality cell region. 


# Dependencies
This module depends on both Loci and CHEM being installed. Loci is an open
source framework developed at Mississippi State University (MSU) by Dr. Ed 
Luke. The framework provides a rule-based programming model and can take 
advantage of massively parallel high performance computing systems. CHEM is a 
full featured open source CFD code with finite-rate chemistry built on the Loci 
framework. CHEM is export controlled under the International Traffic In Arms 
Regulations (ITAR). Both Loci and CHEM can be obtained from the 
[SimSys Software Forum](http://www.simcenter.msstate.edu) hosted by MSU.

# Installation Instructions
First Loci and CHEM should be installed. The **LOCI_BASE** environment
variable should be set to point to the Loci installation directory. The 
**CHEM_BASE** environment variable should be set to point to the CHEM 
installation directory. The installation process follows the standard 
make, make install procedure.

```bash
make
make install
```

# Usage
First the module must be loaded at the top of the **vars** file. 
The user can then specify lower threshold values for volume ratio and
maximum included angle. The user can also set 
**cqrIncludeAdjacentCells** to **1** to include all cells neighboring
those flagged by the thresholds in the locally first order accurate
group.

```
loadModule: cellQualityRemediation

cqrVolumeRatioThreshold: 50
cqrMaxAngleThreshold: 150
cqrIncludeAdjacentCells: 1
```

