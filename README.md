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

On Elixir Registry: [Loctree3](https://bio.tools/tool/RostLab/LocTree3/1.0.8) (this tool) and [Loctree2](https://bio.tools/tool/tum.de/LocTree2/1) (the older previous method; note, these versions do not match with the repository ones).

# Installation

Required environment: you need a Debian repository (tested on Wheezy (7)) or Ubuntu repository (tested on 14). You can also run the prepared [Docker image](#optional-docker).

To install this package, execute the following commands:
```shell
git clone git@github.com:Rostlab/LocTree.git
cd LocTree
aclocal && autoconf && autoheader; automake --add-missing
./configure --prefix=$(pwd)/install
make && make install
```
**loctree3** executable will be in `LocTree/install/bin`

Note: make sure to have the following packages installed: `automake make libconfig-inifiles-perl pp-popularity-contest`

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

# [Optional] Docker

Alternatively, the following docker recipe will create a working machine:

```
FROM ubuntu:14.04
RUN apt-get -y update && apt-get install -y wget unzip automake make libconfig-inifiles-perl pp-popularity-contest
RUN wget -q https://github.com/Rostlab/LocTree/archive/develop.zip && unzip -q develop.zip
RUN cd LocTree-develop && aclocal && autoconf && autoheader; automake --add-missing && ./configure && make && make install
RUN wget -q ftp://ftp.ncbi.nlm.nih.gov/blast/executables/release/LATEST/blast-2.2.26-x64-linux.tar.gz && tar xf blast-2.2.26-x64-linux.tar.gz
RUN /bin/echo -e "[NCBI]\nData=/blast-2.2.26/data/" > ~/.ncbirc && /bin/echo -e "export PATH=$PATH:/blast-2.2.26/bin" >> ~/.bashrc
```

To build the docker image put these previous lines in a file called `Dockerfile` and then run
```
docker build -t loctree-docker .
```
After the building is done you can open a bash shell in the docker image by executing:
```
docker run -ti loctree-docker /bin/bash
```
On this virtual image loctree can be used immediately by running for example:
```
loctree3 -i /usr/local/share/doc/loctree3/examples/arch/ --resfile ./arch_output.lc3 --domain arch
```
