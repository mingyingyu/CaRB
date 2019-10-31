# CaRB - A Crowdsourced Benchmark for Open IE

CaRB : ***C***rowdsourced ***a***utomatic open ***R***elation extraction ***B***enchmark


## Introduction

CaRB is a dataset cum evaluation framework for benchmarking Open Information Extraction systems.

The details of this benchmark are elaborated in our [EMNLP 2019 Paper](http://www.cse.iitd.ernet.in/~mausam/papers/emnlp19.pdf).

### Citing
If you use this software, please cite:
```
@InProceedings{EMNLP2019_4099,
  author    = {Bhardwaj, Sangnie and Aggarwal, Samarth and Mausam},
  title     = {CaRB : A Crowdsourced Benchmark for Open IE},
  booktitle = {Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing (EMNLP)},
  month     = {November},
  year      = {2019},
  address   = {Hong Kong, China},
  publisher = {Association for Computational Linguistics},
  pages     = {(to appear)},
  url       = {http://www.cse.iitd.ernet.in/~mausam/papers/emnlp19.pdf}
}
```

### Contact
Leave us a note at 
```samarthaggarwal2510 (at) gmail (dot) com```

## Requirements

* Python 3
* See required python packages [here](requirements.txt).



## Evaluating an Open IE Extractor

Currently, we support the following Open IE output formats:

* [ClausIE](https://www.mpi-inf.mpg.de/departments/databases-and-information-systems/software/clausie/)
* [OLLIE](http://knowitall.github.io/ollie/)
* [OpenIE-4](https://github.com/allenai/openie-standalone)
* [OpenIE-5](https://github.com/allenai/openie-standalone)
* [PropS](http://u.cs.biu.ac.il/~stanovg/props.html)
* [ReVerb](http://reverb.cs.washington.edu/)
* [Stanford Open IE](http://nlp.stanford.edu/software/openie.html)
* Tab Separated - Read simple tab format file, where each line consists of:
                                sent, prob, pred,arg1, arg2, ...

To evaluate your OpenIE system:

1. Run your extractor over the [dev sentences](data/dev.txt) or [test sentences](data/test.txt) and store the output into "*your_output*.txt"

2. Depending on your output format, you can get a precision-recall curve by running [carb.py](carb.py):
``` 
Usage:
   python carb.py --gold=GOLD_OIE --out=OUTPUT_FILE (--stanford=STANFORD_OIE | --ollie=OLLIE_OIE |--reverb=REVERB_OIE | --clausie=CLAUSIE_OIE | --openiefour=OPENIEFOUR_OIE | --props=PROPS_OIE)

Options:
  --gold=GOLD_OIE              The gold reference Open IE file (by default, it should be under ./oie_corpus/all.oie).
  --out=OUTPUT_FILE            The output file, into which the precision recall curve will be written.
  --clausie=CLAUSIE_OIE        Read ClausIE format from file CLAUSIE_OIE.
  --ollie=OLLIE_OIE            Read OLLIE format from file OLLIE_OIE.
  --openiefour=OPENIEFOUR_OIE  Read Open IE 4 format from file OPENIEFOUR_OIE.
  --openiefive=OPENIEFIVE_OIE  Read Open IE 5 format from file OPENIEFIVE_OIE.
  --props=PROPS_OIE            Read PropS format from file PROPS_OIE
  --reverb=REVERB_OIE          Read ReVerb format from file REVERB_OIE
  --stanford=STANFORD_OIE      Read Stanford format from file STANFORD_OIE
  --tabbed=TABBED_OIE		   Read tabbed format from file TABBED_OIE
```

## Evaluating Existing Systems

In the course of this work we tested the above mentioned Open IE parsers against our benchmark.
We provide the output files (i.e., Open IE extractions) of each of these
systems in [systems_outputs/test](systems_outputs/test).
You can give each of these files to [carb.py](carb.py), to get the corresponding precision recall curve.

For example, to evaluate Stanford Open IE output, run:
```
python carb.py --gold=data/gold/test.tsv --out=dump/OpenIE-4.dat --openiefour=system_outputs/test/openie4_output.txt
```

## Plotting

You can plot together multiple outputs of [carb.py](carb.py), by using [pr_plot.py](pr_plot.py):

```
Usage:
   pr_plot --in=DIR_NAME --out=OUTPUT_FILENAME 

Options:
  --in=DIR_NAME            Folder in which to search for *.dat files, all of which should be in a P/R column format (outputs from benchmark.py).
  --out=OUTPUT_FILENAME    Output filename, filetype will determine the format. Possible formats: pdf, pgf, png
```
