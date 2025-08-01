# gnssir-rt
Software for processing low-cost GNSS-IR water level data. This software accompanies the article ["Real-time water levels using GNSS-IR: a potential tool for flood monitoring"](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2023GL105039) by Purnell et al. (Geophysical Research Letters).

The script [make_gpt.py](./gnssir/make_gpt.py) was taken fron an old version of the repository [gnssrefl](https://github.com/kristinemlarson/gnssrefl).

## Installation
From the command line, clone and cd into the repository root
```
git clone https://github.com/purnelldj/gnssir-rt.git
cd gnssir-rt
```
create and install a venv or conda env as preferred and then install the package using
```
pip install -e .
```

## Usage
Below is an example of how to process one day of data from Saint-Joseph-de-la-Rive.

### Step 1: prepare to analyze test data
Make a directory called data in the repository root
```
mkdir data
```
copy the test data to the data directory
```
unzip tests/testdata/sjdlr.zip -d data/sjdlr
```

### Step 2: process test data
```
gnssir site=sjdlr task=arcs2splines
```
this command should produce the following plot:

![spline output](./images/sjdlr_oneday.png "test output")

### general usage
```
gnssir site=[site] task=[task]
```
* `[site]` corresponds to a config file: `gnssir/configs/site/[site].yaml` (either `sjdlr` or `rv3s`)
* `[task]` is one of `snr2arcs`, `arcsplot` or `arcs2splines`
You can edit the config files as desired, or create a new one.

## Article data
SNR data to go with the paper can be found [here](https://doi.org/10.5281/zenodo.10114719). It can be downloaded using zenodo_get
```
zenodo_get 10.5281/zenodo.10114719
```
Note: this will take a few minutes (~ 1Gb of data)

## SNR data format
The SNR data format is similar to [this format](https://gnssrefl.readthedocs.io/en/latest/pages/file_structure.html#the-snr-data-format), but with differences on fourth and fifth columns:
* instead of seconds of day in the fourth column it is [GPS time](https://docs.astropy.org/en/stable/api/astropy.time.TimeGPS.html)
* the fifth column is L1 SNR (there are only five columns)
