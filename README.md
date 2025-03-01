[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/zadorlab/sella)

# Sella-constraints

This is almost sella==2.0.2. This repository is renamed for the simultaneous use of sella==1.0.0, which allows IRC even in the presence of constraints, and sella==2.0.2, which has excellent constraints handling.

Sella is a utility for finding first order saddle points

An example script
```python
#!/usr/bin/env python3

from ase.build import fcc111, add_adsorbate
from ase.calculators.emt import EMT

from sellac import Sella, Constraints

# Set up your system as an ASE atoms object
slab = fcc111('Cu', (5, 5, 6), vacuum=7.5)
add_adsorbate(slab, 'Cu', 2.0, 'bridge')

# Optionally, create and populate a Constraints object.
cons = Constraints(slab)
for atom in slab:
    if atom.position[2] < slab.cell[2, 2] / 2.:
        cons.fix_translation(atom.index)

# Set up your calculator
slab.calc = EMT()

# Set up a Sella Dynamics object
dyn = Sella(
    slab,
    constraints=cons,
    trajectory='test_emt.traj',
)

dyn.run(1e-3, 1000)
```

If you are using Sella or you wish to use Sella, let me know!

## Documentation

For more information on how to use Sella, please check the [wiki](https://github.com/zadorlab/sella/wiki).

## Support

If you need help using Sella, please visit our [gitter support channel](https://gitter.im/zadorlab/sella),
or open a GitHub issue.

## Acknowledgments

This work was supported by the U.S. Department of Energy, Office of Science, Basic Energy Sciences, Chemical Sciences, Geosciences and Biosciences Division, as part of the Computational Chemistry Sciences Program.
