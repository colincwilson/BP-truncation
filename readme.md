# Modeling truncation in Brazilian Portuguese

By [Mike Pham](http://www.mikettpham.com/) and [Jackson Lee](http://jacksonllee.com/)

A full paper is currently being prepared,
which is a substantially expanded and revised version of the brief write-up
as a
[technical report (TR-2014-15, UChicago Computer Science)](https://newtraell.cs.uchicago.edu/research/publications/techreports/TR-2014-15).

## Contents

- ``main.py``: Python script for running the different truncation models over the data files in the ``data/`` folder

- ``data/``: directory for datasets

    * ``pt_br_full.txt``: Brazilian Portuguese lexicon (8.7 MB)
    * ``gold_standard.txt``: gold standard nouns with attested truncation,
      all annotated with predictions from models such as the binary foot models

- ``plots_for_words/``: directory for output plots for individual words for log(left-complete counts) and log(right-complete counts)

- ``results/``: directory for output files
  * error details in CSV
  * error distribution boxplot
  * evaluation
  * L- and R-complete counts for individual in LaTeX and PDF
  * R code for making individual plots for test words

- ``readme.md``: this readme file

## Requirements

Python 3.4 or above is required.
A Unix-based system (Linux or Mac) is assumed.

[NumPy](http://www.numpy.org/), [SciPy](http://www.scipy.org/),
[Pandas](http://pandas.pydata.org/),
and [Seaborn](https://stanford.edu/~mwaskom/software/seaborn/)
are required to run ``main.py``.
A great Python distribution that comes with these packages (and many others)
is [Anaconda](https://www.continuum.io/downloads).

*Optional* -- If the following commands are recognized in your path environment:

- ``Rscript``: ``plot_word.R`` (generated by ``main.py``) is run and the plots for
  individual words are saved in ``plots_for_words/``.
  
- ``xelatex``: ``individual_word_details.tex`` (generated by ``main.py``)
  is compiled and the resultant PDF is saved in ``results/``.

``Rscript`` comes from R, whereas ``xelatex`` comes from a LaTeX distribution
(such as ``texlive-full``).

## Download

Download this repository to your local drive by one of these two methods:

* Download and unzip https://github.com/JacksonLLee/BP-truncation/archive/master.zip

* Clone this repository:

    ```
    $ git clone https://github.com/JacksonLLee/BP-truncation.git
    $ cd BP-truncation
    ```

## Usage

``main.py`` can take optional arguments.
 The argument ``-h`` brings up the help page with details of these arguments:

```
$ python main.py -h
usage: main.py [-h] [-f] [-l] [-r] [-d] [-x LEXICON] [-g GOLDSTANDARD]

Modeling truncation in Brazilian Portuguese, by Mike Pham and Jackson Lee

optional arguments:
  -h, --help            show this help message and exit
  -f, --freqtoken       Use token frequencies in lexicon (default: False)
  -l, --latex           Compile the output LaTeX file (default: False)
  -r, --run_r_script    Run R script (default: False)
  -d, --digraphsfixed   Change orthographic digraphs into monographs (default:
                        False)
  -x LEXICON, --lexicon LEXICON
                        Lexicon file (default: data/pt_br_full.txt)
  -g GOLDSTANDARD, --goldstandard GOLDSTANDARD
                        Gold standard file (default: data/gold_standard.txt)
```

The sample output files included in this repository are generated by this command:

```
$ python main.py -lr
```
 
This command has most of the default settings as described in the help page
shown above, except that R code is run and LaTeX compilation is triggered.
If you don't want to run R and LaTeX, simply run ``python main.py``
with no other arguments.

If, for instance, you'd like to make use of word token frequency information
in the models that involve right-completes and left-completes,
you should run ``python main.py -flr`` (still running R and LaTeX).
All output files for this command bear the suffix "-tokenfreq".

To activate orthographic digraph replacements, run ``python main.py -dlr``.
All output files are suffixed by "-nodigraphs".

The arguments ``--lexicon`` and ``-goldstandard``
may be used to override the default lexicon
and gold standard files, respectively.
See the sections below on their file format.

## Lexicon

The lexicon file is a plain text file
where each line begins with a word, and then a space/tab, and finally
the frequency count of that word in some corpus.
The ordering of the words in the lexicon file does not matter.
Here are the first ten lines of the 
the default lexicon file in this repository
(``data/pt_br_full.txt``):

```
que 12021478
não 9712854
o 9578625
de 8089861
a 7188507
é 6843557
você 6211533
e 5863939
eu 5741437
um 4589127
```

## Gold standard file

The gold standard file is a plain text file
where each line has one original (untruncated) word, and then a
space/tab, and finally the truncated form (TF) of that original word;
the TF is just for reference and is not used by ``main.py`` in any way.
The original word is annotated by the following symbols:

* ``|``: where the true truncation point is for forming the truncated
  stem (TS).
  For instance, the TS for *adrenalina* (see below) is *adren*.
* ``$``: where the truncation point is as predicted by the binLR model.
* ``#``: where the truncation point is as predicted by the binRL model.

Here are the first ten lines of the default gold standard file in this
repository (``data/gold_standard.txt``):

```
adr$en|#alina	adrena
an$alf|#abeto	analfa
bat$#er|ista	batera
bel$e|z#a	belê
berm|$ud#a	bermas
bij$#u|teria	biju
bis|$av#ó	bisa
bob|$eir#a	bobis
bot$equ|#im	boteco
burg|$#ês	burga
```
