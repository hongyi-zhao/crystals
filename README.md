crystals
========
[![Documentation Status](https://readthedocs.org/projects/crystals/badge/?version=master)](https://crystals.readthedocs.io/) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/LaurentRDC/crystals?branch=master&svg=true)](https://ci.appveyor.com/project/LaurentRDC/crystals) [![PyPI Package latest release](https://img.shields.io/pypi/v/crystals.svg)](https://pypi.python.org/pypi/crystals) [![Conda-forge Version](https://img.shields.io/conda/vn/conda-forge/crystals.svg)](https://anaconda.org/conda-forge/crystals) [![Supported Python versions](https://img.shields.io/pypi/pyversions/crystals.svg)](https://pypi.python.org/pypi/crystals)

`crystals` is a library of data structure and algorithms to manipulate
abstract crystals in a Pythonic way. `crystals` helps with reading
crystallographic files (like .cif and .pdb), provides access to atomic
positions, scattering utilities, and allows for symmetry determination.
Although `crystals` can be used on its own, it was made to be integrated
into larger projects (like
[scikit-ued](https://github.com/LaurentRDC/scikit-ued)).

Take a look at the [documentation](https://crystals.readthedocs.io/) for
more information.

Usage example
-------------

`crystals` is all about constructing crystals and getting information
about the resulting object. Crystals can be built from a variety of
sources:

-   From files on disk, such as Crystallography Information Files (CIF)
    or Place-Wave Self-Consistent Field calculations (PWSCF);
-   From the internal database of over 90 structure files (mostly
    elemental crystals);
-   From online databases, such as the [RCSB Protein
    DataBank](http://www.rcsb.org/) or the [Crystallography Open
    Database](http://www.crystallography.net/cod/).

Here\'s a quick example of building a crystal from the internal
database:

```python
    >>> from crystals import Crystal
    >>>
    >>> vo2 = Crystal.from_database('vo2-m1')
    >>> print(vo2)     # Short string representation
    < Crystal object with following unit cell:
        Atom O  @ (0.90, 0.79, 0.80)
        Atom O  @ (0.90, 0.71, 0.30)
        Atom O  @ (0.61, 0.31, 0.71)
        Atom O  @ (0.39, 0.69, 0.29)
        Atom O  @ (0.61, 0.19, 0.21)
        Atom O  @ (0.10, 0.29, 0.70)
        Atom O  @ (0.10, 0.21, 0.20)
        Atom O  @ (0.39, 0.81, 0.79)
        Atom V  @ (0.76, 0.03, 0.97)
        Atom V  @ (0.76, 0.48, 0.47)
        ... omitting 2 atoms ...
    Lattice parameters:
        a=5.743Å, b=4.517Å, c=5.375Å
        α=90.000°, β=122.600°, γ=90.000°
    Chemical composition:
        O: 66.667%
        V: 33.333%
    Source:
        (...omitted...)\crystals\cifs\vo2-m1.cif >
```

Symmetry information is also readily available:

```python
    >>> print(vo2.symmetry())
    {'international_symbol': 'P2_1/c', 
     'hall_symbol': '-P 2ybc', 
     'hm_symbol': 'P121/c1',
     'international_number': 14, 
     'hall_number': 81, 
     'international_full': 'P 1 2_1/c 1', 
     'pointgroup': 'C2h'}
```

### Command-line script

`crystals` comes with command-line utilities. The most important of them
is the `crystals info` command-line program, which will give you
information on a crystal.

For example, the equivalent of the usage example above is as follows:

```bash
    > crystals info vo2-m1
    Crystal object with following unit cell:
        Atom O  @ (0.10, 0.29, 0.70)
        Atom O  @ (0.90, 0.79, 0.80)
        Atom O  @ (0.39, 0.69, 0.29)
        Atom O  @ (0.39, 0.81, 0.79)
        Atom O  @ (0.61, 0.19, 0.21)
        Atom O  @ (0.61, 0.31, 0.71)
        Atom O  @ (0.10, 0.21, 0.20)
        Atom O  @ (0.90, 0.71, 0.30)
        Atom V  @ (0.24, 0.97, 0.03)
        Atom V  @ (0.24, 0.53, 0.53)
        Atom V  @ (0.76, 0.48, 0.47)
        Atom V  @ (0.76, 0.03, 0.97)
    Lattice parameters:
        a=5.743Å, b=4.517Å, c=5.375Å
        α=90.000°, β=122.600°, γ=90.000°
    Chemical composition:
        O: 66.667%
        V: 33.333%
    Source: 
        (...omitted...)\crystals\cifs\vo2-m1.cif
    Symmetry information:
        International symbol 
                    (short) ..... P2_1/c
                    (full) ...... P 1 2_1/c 1
        International number .... 14
        Hermann-Mauguin symbol .. P121/c1
        Pointgroup .............. C2h
        Hall Number ............. 81
        Centering ............... CenteringType.primitive
```

`crystals` will guess what the input means. You can pass a filename, or
database entry. See `crystals --help` for more details.

Installation
------------

`crystals` is available on the Python Package Index:

    pip install crystals

For users of the conda package manager, `crystals` is also available
from the conda-forge channel:

    conda install -c conda-forge crystals

### From source

`crystals` can also be installed from source:

    git clone https://github.com/LaurentRDC/crystals.git
    cd crystals
    python setup.py install

You can install the latest development version using `pip` as well:

    python -m pip install git+git://github.com/LaurentRDC/crystals.git

To build documentation, you will need a few more packages, listed in
`dev-requirements.txt`. For example, to build documentation from source:

    git clone https://github.com/LaurentRDC/crystals.git
    cd crystals
    pip install -r dev-requirements.txt
    python setup.py build_sphinx

Documentation
-------------

The documentation, including a user guide as well as detailed reference,
is available here: <https://crystals.readthedocs.io/>

Development
-----------

Tests can be run with the standard library\'s `unittest`
module:

    python -m unittest discover

Some optional tests might be skipped if dependencies are not installed,
e.g. [ASE](https://wiki.fysik.dtu.dk/ase/).

Citations
---------

As this package is a spinoff from `scikit-ued`, please consider citing
the following publication if you find `crystals` useful:

> L. P. René de Cotret, M. R. Otto, M. J. Stern. and B. J. Siwick, *An open-source software ecosystem for the interactive exploration of ultrafast electron scattering data*, Advanced Structural and Chemical Imaging 4:11 (2018) [DOI: 10.1186/s40679-018-0060-y.](https://ascimaging.springeropen.com/articles/10.1186/s40679-018-0060-y)

Underlying algorithms provided by `spglib` are described in the
following publication:

> A. Togo and I. Tanaka, *spglib: a software library for crystal symmetry search*. [https://arxiv.org/abs/1808.01590](https://arxiv.org/abs/1808.01590) (written at version 1.10.4).

Structure parsing from CIF files has been tested for correctness against
CIF2CELL, detailed here:

> Torbjorn Bjorkman, *CIF2Cell: Generating geometries for electronic structure programs*, Computer Physics Communications 182, 1183-1186 (2011) [DOI: 10.1016/j.cpc.2011.01.013](https://doi.org/10.1016/j.cpc.2011.01.013)

Structure parsing from PDB files has been tested for correctness against
`Bio.PDB`, detailed here:

> Hamelryck, T., Manderick, B. *PDB parser and structure class implemented in Python*. Bioinformatics 19: 2308–2310 (2003)

Atomic weights are reported in the following publication:

> Meija, J., Coplen, T., Berglund, M., et al. (2016). *Atomic weights of the elements 2013* (IUPAC Technical Report). Pure and Applied Chemistry, 88(3), pp. 265-291. Retrieved 30 Nov. 2016, [DOI:10.1515/pac-2015-0305](https://doi.org/10.1515/pac-2015-0305)

Aknowledgements
---------------

This package depends on the work of some amazing people. Of note are the
[spglib contributors](https://github.com/atztogo/spglib).

Support / Report Issues
-----------------------

All support requests and issue reports should be [filed on Github as an
issue](https://github.com/LaurentRDC/crystals/issues).

License
-------

`crystals` is made available under the BSD 3-clause license. For more
details, see [LICENSE](https://github.com/LaurentRDC/crystals/blob/master/LICENSE).

Related projects
----------------

-   Streaming operations on NumPy arrays are available in the [npstreams
    package](https://pypi.org/pypi/npstreams).
-   Interactive exploration of ultrafast electron diffraction data with
    the [iris-ued package](https://pypi.org/project/iris-ued/).
-   Data structures and algorithms to handle ultrafast electron
    scattering data in the [scikit-ued
    package](https://pypi.org/project/scikit-ued).
