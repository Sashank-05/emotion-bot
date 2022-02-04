# Demo Code for "Talking Head Anime from a Single Image"

You may want to check out the much more capable Version 2 of the same software: http://github.com/pkhungurn/talking-head-anime-2-demo
  
This repository contains code for two applications that make use of the neural network system in the [Talking Head Anime from a Single Image](http://pkhungurn.github.io/talking-head-anime/) project:  
  
* The *manual poser* allows the user to pose an anime character by manually manipulating sliders.
* The *puppeteer* makes an anime character imitate the head movement of the human capture by a webcam feed.

## Try the Manual Poser on Google Colab

If you do not have the required hardware (discussed below) or do not want to download the code and set up an environment to run it, click [![this link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Sashank-05/emotion-bot/tha_colab.ipynb) to try running the manual poser on [Google Colab](https://research.google.com/colaboratory/faq.html).

## Hardware Requirements

As with many modern machine learning projects written with PyTorch, this piece of code requires **a recent and powerful Nvidia GPU** to run. I have personally run the code on a Geforce GTX 1080 Ti and a Titan RTX.

Also, the peppeteer tool requires a webcam.

## Dependencies

* Python >= 3.6
* pytorch >= 1.4.0
* dlib >= 19.19
* opencv-python >= 4.1.0.30
* pillow >= 7.0.0
* numpy >= 1.17.l2

If you install these packages, you should be all good.

## Recreating Python Environment with Anaconda

If you use [Anaconda](https://www.anaconda.com/), you also have the option of recreating the Python environment that can be used to run the demo. Open a shell and change directory to the project's root. Then, run the following command:

> `conda env create -f environment.yml`

This should download and install all the dependencies. Keep in mind, though, that this will require several gigabytes of your storage. After the installation is done, you can activate the new environment with the following command:

> `conda activate talking-head-anime`

Once you are done with the environment, you can deactivate it with:

> `conda deactivate`

## Prepare the Data

After you cloned this repository to your machine's storage, you need to download the models: 

* Download the main models from [this link](https://drive.google.com/open?id=1ajHViqyLDKFKfBtGPE5cbSGcMNa8rz8k). Unzip the file into the `data` directory under the project's root. The models are released separately with the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/legalcode).
* Download `shape_predictor_68_face_landmarks.dat` and save it to the `data` directory. You can download the bzip archive from [here](https://github.com/davisking/dlib-models). Do not forget to uncompress.

Once the downloading is done, the data directory should look like the following:

```
+ data
  + illust
    - placeholder.txt
    - waifu_00_256.png
    - waifu_01_256.png
    - waifu_02_256.png
    - waifu_03_256.png
    - waifu_04_256.png
  - combiner.pt
  - face_morpher.pt
  - placeholder.txt
  - shape_predictor_68_face_landmarks.dat
  - two_algo_face_rotator.pt
```

To play with the demo, you can use the 5 images I included in the `data/illust`. Or, you can prepare some character images by yourself. Images that can be animated must satisfy the following requirements:
* It must be in PNG format.
* It must be of size 256 x 256.
* The head of the character must be contained in the center 128 x 128 box.
* It must have 4 channels (RGBA).
* Pixels that do not belong to the character's body must have value (0,0,0,0). In other words, the background must be transparent.

For more details, consult Section 4 of the [web site of the project writeup](https://pkhungurn.github.io/talking-head-anime/). You should save all the images in the `data/illust` directory. One good way to get character images is to generate one with [Waifu Labs](https://waifulabs.com/) and edit the image to fit the above requirements.

## Running the Program

Change directory to the root directory of the project. To run the manual poser, issue the following command in your shell:

> `python app/manual_poser.py`

To run the puppeteer, issue the following command in your shell:

> `python app/puppeteer.py`


