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
**loctree3** executable will be in `LocTree/install/bin`

# Usage

To use **loctree3** it is necessary to have blastpgp, which can be obtained by downloading the package *blast-2.2.26* for the corresponding platform from the following FTP: ftp://ftp.ncbi.nlm.nih.gov/blast/executables/release/LATEST/

For example for a Linux x64 architecture it can be installed with the following commands:
```
wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/release/LATEST/blast-2.2.26-x64-linux.tar.gz
tar xf blast-2.2.26-x64-linux.tar.gz
echo -e "[NCBI]\nData=$(pwd)/blast-2.2.26/data/" > ~/.ncbirc
```
The location of the **blastpgp** binaries must also be added tho the PATH environment variable:
```
export PATH=$PATH:$(pwd)/blast-2.2.26/bin
```
Now it should be possible to run **loctree3**. For example:
```
cd LocTree/install/bin
./loctree3 -i ../share/doc/loctree3/examples/arch/ --resfile ./arch_output.lc3 --domain arch
```
will generate the output file *arch_output.lc3* with the predicted sub-cellular localization

Reading the man page of loctree3, which offers additional information, can be done the following way:
```
MANPATH=LocTree/install/share/man/ man loctree3
```
