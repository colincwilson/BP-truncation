# Modeling truncation in Brazilian Portuguese

By Mike Pham and Jackson Lee

A full paper is currently being prepared,
which is a substantically expanded and revised version of the brief write-up
as a
[technical report (TR-2014-15, UChicago Computer Science)](https://newtraell.cs.uchicago.edu/research/publications/techreports/TR-2014-15).

## Contents

- ``main.py``: Python script for running the different truncation models over the data files in the ``data/`` folder

- ``data/``:

    * ``pt_br_orthofix*``: Brazilian Portuguese lexicon (two versions)
    * gold standard nouns with attested truncation (available in various formats for different annotations regarding binary foot model predictions)

- ``plots_words/``: output plots for individual words for log(left-complete counts) and log(right-complete counts)

- ``plots_errors/``: output plots of error distributions

- ``outlatex*``: sameple output LaTeX files

- ``output*``: sample CSV output file

- ``plots*``: sample output R scripts

- ``readme.md``: this readme file


## Usage

Download this repository to your local drive by one of these two methods:

* Download and unzip https://github.com/JacksonLLee/BP-truncation/archive/master.zip

* Clone this repository:

    $ git clone https://github.com/JacksonLLee/BP-truncation.git
    $ cd BP-truncation

After this repository is downloaded, run the truncation models for the accompanying datasets:

    $ python3 main.py

Once this Python script is run, output files ``outlatex*`` (LaTeX output), ``output*`` (CSV output), and ``plots*`` (R scripts) are generated at the same directory. In addition, output plots of interest are in the subdirectories ``plots_words/`` and ``plots_errors/``.

*LaTeX and R outputs:*

If you are on a Unix-like system (Linux or Mac)
and the command line path environment recognizes
the commands ``xelatex`` and ``Rscript``,
then the generated ``.tex`` will be compiled and the ``.R`` file will be run by R.
If you are on Windows or if for other reasons the commands ``xelatex`` and ``Rscript``
are unavailable, then ``.tex`` and ``.R`` can be run by other non-command line means of your choice.

