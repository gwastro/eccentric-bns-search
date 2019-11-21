# Search for Eccentric Binary Neutron Star Mergers in the first and second observing runs of Advanced LIGO
**Alexander H. Nitz<sup>1,2</sup>, Amber Lenon<sup>3</sup>, Duncan A. Brown<sup>4</sup>**


 <sub>1. [Albert-Einstein-Institut, Max-Planck-Institut for Gravitationsphysik, D-30167 Hannover, Germany](http://www.aei.mpg.de/obs-rel-cos)</sub>  
 <sub>2. Leibniz Universitat Hannover, D-30167 Hannover, Germany</sub>  
 <sub>3. Department of Physics and Astronomy, West Virginia University, Morgantown WV 26506, USA
 <sub>4. Department of Physics, Syracuse University, Syracuse, NY 13244, USA</sub>

## Introduction ##

We present a search for gravitational waves from merging binary neutron stars which have nonnegligible eccentricity as they enter the LIGO observing band. We use the public Advanced LIGO data which covers the period from 2015 through 2017 and contains ∼ 164 days of LIGO-Hanford and LIGO-Livingston coincident observing time. The search was conducted using matched-filtering based on the PyCBC toolkit. We find no significant binary neutron star candidates beyond GW170817, which
has previously been reported by searches in binaries in circular orbits. We place a 90 % upper limit of∼ 1700 mergers Gpc−3Yr−1 for eccentricities . 0.45 at a reference dominant-mode gravitational-wave frequency of 10 Hz. The detection of an eccentric neutron star merger given the current sensitivity of gravitational-wave observatories would require more optimistic formation rates than predicted for existing scenarios, we estimate that only half a year of observing by Cosmic Explorer would constrain the current models.

The catalog is stored in the file '1-ECCBNS.hdf'. There are a variety of tools to access [hdf files](https://www.hdfgroup.org/) from numerous computing languages. Here we will focus on access through python and [h5py](www.h5py.org).

## Analysis Details ##
Details of the analysis are available in this [preprint paper]() and the configuration files needed to create the analysis workflows are provided in the [workflow/configuration](https://github.com/gwastro/eccentric-bns-search/tree/master/workflow/configuration) directory.

## Accessing the Catalog: 1-ECCBNS.hdf ##

There are two datasets within the file, `/complete` and `/bbh`. The `complete` set is the full dataset from our analysis. The `bbh` set includes BBH candidates from a select portion of the analysis. See the 1-OGC paper for additional information. 


```python
import h5py

catalog = h5py.File('./1-ECCBNS.hdf', 'r')

# Accessing a column by name
ranking_values = catalog['stat'][:]
```


##### File format #####
The file constains a set of named columns. Some of these columns give information specific to either the 
LIGO Hanford or Livingston detectors. Where this is the case, the name of the column is prefixed with either a `H1` or `L1`.

| Key           | Description                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| name          | The designation of the candidate event. This is of the form 150812+12:23:04UTC.                                                     |
| far           | The rate of false alarms with a ranking statistic as large or larger than this event. The unit is yr^-1.                                                                                                           |
| stat          | The value of the ranking statistic for this candidate event.                                                                                       |
| mass1         | The component mass of one compact object in the template waveform which found this candidate. Units in detector frame solar masses. |
| mass2         | The component mass of the template waveform which found this candidate. Units in detector frame solar masses.                       |
| eccentricity       | The eccentricity parameter of the binary merger    |
| {H1/L1}_end_time   | The time in GPS seconds when a fiducial point in the signal passes throught the detector. Typically this is near the time of merger.                                                                                                                              |                                                                                                                           |
| {H1/L1}_snr        | The amplitude of the complex matched filter signal-to-noise observed.                                                                                                                                    |
| {H1/L1}_coa_phase        | The phase (angle) of the complex matched filter signal-to-noise observed.                                                          |
| {H1/L1}_reduced_chisq |  Value of the signal consistency test defined in this [paper](https://arxiv.org/abs/gr-qc/0405045). This is not calculated for all candidate events. In this case a value of 0 is substituted.                                                                                                                                  |
| {H1/L1}_sigmasq       |   The integral of the template waveform divided by the power spectral density.


![Creative Commons License](https://i.creativecommons.org/l/by-sa/3.0/us/88x31.png "Creative Commons License")

This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 United States License](http://creativecommons.org/licenses/by-sa/3.0/us/).

We encourage use of these data in derivative works. If you use the material provided here, please cite the paper using the reference:

```
@article{Nitz:2019XXX,
      author         = "Alexander H. Nitz, Amber Lenon, Duncan A. Brown",
      title          = "{}",
      year           = "2019",
      eprint         = "XXXXXXXXX",
      archivePrefix  = "arXiv",
      primaryClass   = "gr-qc",
      SLACcitation   = "%%CITATION = ARXIV:XXXXXXXXX;%%"
}
```


## Acknowledgments ##
We thank Nico Yunes and Blake Moore for their assistance and insight. We acknowledge the Max Planck
Gesellschaft for support and the Atlas cluster computing
team at AEI Hannover. This research has made use of
data, software and/or web tools obtained from the Gravitational Wave Open Science Center (https://www.gwopenscience.org), a service of LIGO Laboratory, the
LIGO Scientific Collaboration and the Virgo Collaboration. LIGO is funded by the U.S. National Science
Foundation. Virgo is funded by the French Centre National de Recherche Scientifique (CNRS), the Italian Istituto Nazionale della Fisica Nucleare (INFN) and the
Dutch Nikhef, with contributions by Polish and Hungarian institutes.
