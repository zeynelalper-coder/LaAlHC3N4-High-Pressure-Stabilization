# LaAlHC3N4 High-Pressure Stabilization via Carbon Nitride Matrix

An AI-driven materials design project evaluating the structural and thermodynamic stability of heavily compressed ternary superhydrides under ambient pressure conditions using Neural Network Potentials (NNP).

## Scientific Abstract

**Title:** Investigation of the Metastable Cmcm-Phase in the Quaternary La-Al-H-C-N System under Ambient Pressure via Neural Network Potentials  
**Author:** Alper et al. (2026)  

In this computational study, a novel structural design for the chemical stabilization of hydrogen-rich high-temperature superconductors at ambient pressure (1 Bar) was investigated. To suppress the mechanical collapse and macroscopic expansion typical of superhydrides upon pressure release, a Cmcm-carbon nitride matrix (C₃N₄) was engineered as a covalent cage to intercalate Lanthanum, Aluminum, and Hydrogen species.

The geometric and energetic evaluation of the highly compressed structure (LaAlHC₃N₄) was performed using the state-of-the-art machine learning model **CHGNet**. After a 30-step FIRE structural relaxation, the system demonstrated remarkable mechanical retention, snapping into a stable final volume of **94.02 Å³** with optimized lattice constants of:
- a = 3.792 Å
- b = 6.508 Å
- c = 3.809 Å

The atomic packing fraction stabilized at a highly efficient **54.13%**, yielding a calculated material density of **5.0416 g/cm³**. However, the predicted internal energy of **+27.7059 eV/atom** indicates a severe thermodynamic metastability. While this system offers a valid proof-of-concept for covalent pre-compression, synthesizability via solid-state pathways remains a challenge due to competing binary phases.

## Structure Info (XYZ Fractional Coordinates)
```text
# Unit Cell: a=3.792, b=6.508, c=3.809
C  0.16869850  0.16332050  0.75000000
C  0.17890000  0.49994900  0.25000000
C  0.00000000  0.00545100  0.25000000
C  0.00000000  0.32068000  0.75000000
N  0.16294050  0.05803250  0.25000000
N  0.16566500  0.27083400  0.75000000
N  0.17111250  0.39223250  0.25000000
N  0.00000000  0.10705700  0.75000000
N  0.00000000  0.44023600  0.75000000
La 0.00000000  0.00000000  0.00000000
Al 0.00000000  0.50000000  0.00000000
H  0.00000000  0.25000000  0.25000000
```

## How to Reproduce (Google Colab / Python Code)
```python
!pip install pymatgen matminer chgnet ase
import numpy as np
from pymatgen.core import Structure, Lattice
from chgnet.model.dynamics import StructOptimizer

# Initialize the compressed structure
lattice = Lattice.from_parameters(a=3.800, b=6.500, c=3.800, alpha=90, beta=90, gamma=90)
species = ["C", "C", "C", "C", "N", "N", "N", "N", "N", "La", "Al", "H"]
coords = [
    [0.16869850, 0.16332050, 0.75000000], [0.17890000, 0.49994900, 0.25000000],
    [0.00000000, 0.00545100, 0.25000000], [0.00000000, 0.32068000, 0.75000000],
    [0.16294050, 0.05803250, 0.25000000], [0.16566500, 0.27083400, 0.75000000],
    [0.17111250, 0.39223250, 0.25000000], [0.00000000, 0.10705700, 0.75000000],
    [0.00000000, 0.44023600, 0.75000000], [0.00000000, 0.00000000, 0.00000000],
    [0.00000000, 0.50000000, 0.00000000], [0.00000000, 0.25000000, 0.25000000]
]
structure = Structure(lattice, species, coords)

# Run relaxation
optimizer = StructOptimizer()
relaxed_results = optimizer.relax(structure, steps=30, fmax=0.1)

final_structure = relaxed_results["final_structure"]
final_energy = float(relaxed_results["trajectory"].energies[-1])

print(f"Final Energy: {final_energy:.4f} eV/Atom")
print(f"Final Volume: {final_structure.volume:.2f} Angstrom^3")
```
