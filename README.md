# Compressed Sensing using Generative Models

This repository provides code to reproduce results from the paper: [Compressed Sensing using Generative Models](https://arxiv.org/abs/1703.03208)

### Steps to reproduce the results:
---

#### Preliminaries
---

Download the datasets
```shell
$ python download.py mnist
$ python download.py celebA
```

Make a new folder ```data/celebAtest``` and put some images in that folder. These images will be used for testing the algorithms. The list of images **not** used while training the model can be found [here](https://drive.google.com/open?id=0B0ox77cWXKmLb2pscng0dWlrMjg).

Download pretrained models from <https://drive.google.com/open?id=0B0ox77cWXKmLLUhtWEt3RGdpczg> and put them in ```models/```

To use wavelet based estimators, you need to run ```$ python ./src/wavelet_basis.py``` to create the basis matrix.

#### Experiments
---
These are the supported experiments:

1. Reconstruction from Gaussian measurements
2. Super-resolution
3. Reconstruction for images in the span of the generator (gen-span)
4. Quantifying representation error (projection)
5. Inpainting

For a quick demo of these experiments on MNIST, run ```$ python ./quick_scripts/mnist_{expt}.sh```. For quick demo on celebA, identify an image on which you wish to run it, and run ```$ python ./quick_scripts/celebA_{expt}.sh /path/to/image```

To reproduce the quantitative results, follow these steps:

1. Identfy a dataset you would like to get the quantitative results on. Locate the file ```./quant_scripts/{dataset}_reconstr.sh```.

2. Change ```BASE_SCRIPTS``` in ```src/create_scripts.py``` to be the same as given at the top of ```./quant_scripts/{dataset}_reconstr.sh```.

3. Optionally, comment out the parts of ```./quant_scripts/{dataset}_reconstr.sh``` that you don't want to run.

4. Run  ```$ ./{dataset}_reconstr.sh```. This will create a bunch of ```.sh``` files in the ```./scripts/``` directory, each one of them for a different parameter setting.

5. Start running these scripts.
    - You can run ```$ ./utils/run_sequentially.sh``` to run them one by one.
    - Alternatively use ```$ ./utils/run_all_by_number.sh``` to create screens and start proccessing them in parallel. [REQUIRES: gnu screen][WARNING: This may overwhelm the computer]. You can use ```$ ./utils/stop_all_by_number.sh``` to stop the running processes, and clear up the screens started this way.

6. These scripts will save the results to appropriately named directories. To get the plots, see ```src/metrics.ipynb```. Reconstructed images, can be found in ```estimated/```. To get the matrix of images (as in the paper), see ```src/view_est_{dataset}.ipynb```.
