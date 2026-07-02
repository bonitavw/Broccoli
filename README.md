<p align="center">
  <img width="300" height="auto" src="./images/logo_broccoli.png">
</p>

## Overview

Broccoli is designed to infer with high precision orthologous groups and pairs of proteins using a mixed phylogeny-network approach. Briefly, Broccoli performs ultra- fast phylogenetic analyses on most proteins and builds a network of orthologous relationships. Orthologous groups are then identified from the network using a parameter-free machine learning algorithm (label propagation). Broccoli also detects chimeric proteins resulting from gene-fusion events and assigns these proteins to the corresponding orthologous groups.

__Reference:__ <a href="https://academic.oup.com/mbe/advance-article/doi/10.1093/molbev/msaa159/5865275">Broccoli: combining phylogenetic and network analyses for orthology assignment</a>

<p align="center">
  <img width="650" height="auto" src="./images/overview_broccoli.png">
</p>

## Requirements

To run Broccoli, you need (see the [**manual**](manual_Broccoli_v1.2.pdf) for installation advices):

- a Unix system (MacOS or Linux)
- Python version 3.6 or above
- <a href="https://github.com/etetoolkit/ete">ete3 library</a>
- <a href="https://github.com/bbuchfink/diamond">Diamond</a> version 0.9.30 or above
- <a href="http://www.microbesonline.org/fasttree/">FastTree</a> version 2.1.11 or above (**single-thread version**)

### Installation via pixi

```
pixi lock
pixi info # We get information about the environment
pixi shell # Our shell is the environment
```

## Running Broccoli

All parameters and options are available using the `-help` argument (see also the [**manual**](manual_Broccoli_v1.2.pdf) for more details):

```
python broccoli.py -help
```

To test Broccoli with the small example dataset present in the directory `example_dataset` (30 sec to 1mn):

```
python broccoli.py -dir example_dataset
```

Broccoli will store the temporary and output files in 4 directories named `dir_step1` to `dir_step4` (one for each step) located in the current directory.

If a run is interrupted, or you want to change the parameters of a later step without redoing earlier ones, run Broccoli again from the same directory with the `-resume` option: any step whose `dir_stepN` output is already complete (marked internally by a `.broccoli_done` file written at the end of a successful step) will be skipped. If an earlier requested step has to rerun (its marker is missing, or you deleted it to force a rerun), all later requested steps automatically rerun too, since they depend on that step's output. Note that `-resume` does not detect parameter changes between runs for steps it decides to skip — delete the relevant `dir_stepN` directory (or just its `.broccoli_done` marker) to force that step to rerun with new parameters.

## Licence

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see http://www.gnu.org/licenses/.

See "LICENSE" for full terms and conditions of usage.
