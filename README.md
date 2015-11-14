# Package Information

Development year: 2013

Authors:
* Tatyana Goldberg <goldberg@rostlab.org>
* Maximilian Hecht <hecht@rostlab.org>
* Tobias Hamp <hampt@rostlab.org>
* Burkhard Rost <rost@rostlab.org>

Programming language: Perl

Methodology used: 
* The method predicts three localization classes in Archaea, six in Bacteria, and 18 in Eukaryota.
* Incorporation of annotation by sequence homology (PSI-BLAST searches)
* Printable SVM probability scores along the prediction path of a LocTree2 tree

# Installation

To install this package, execute the following commands:
```
git clone git@github.com:Rostlab/LocTree.git
cd LocTree
aclocal && autoconf && autoheader; automake --add-missing
./configure --prefix=$(pwd)/install
make && make install
```
loctree3 executable will be in `LocTree/install/bin`
