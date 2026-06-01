# Toward Generalizable AI-Generated Image Detection with a New Realistic Datset 
**Thai Ngoc Toan Truong, Ji Li, Kai Wang**

  GIPSA-lab, Univ. Grenoble Alpes, CNRS, Grenoble INP


This repository is the official repository of the RealAI benchmark. 

This repository contains the RealAI dataset and the evaluated methods.

If this project helps you, please fork, watch, and give a star to this repository.   


**RealAI** is a realistic and diverse AI-generated image (AIGI) dataset designed to reflect real-world detection challenges.  
It improves upon previous datasets through:

- **High realism** in generated fake images  
- **Coverage across GAN, Diffusion, and Autoregressive (AR) models**  
- **Balanced real vs. fake samples**  
- **Wide semantic diversity**  
- **Challenging evaluation of generalization to unseen generators**

<div align=center>
<img src='Images/images.png' width=750>
</div>

## Dataset

Each folder contains compressed files. After unzip the file, files under the data root directory can be organized as follows. The ai folder contains the AI-generated images, and the nature folder contains the collected images from ImageNet.

```
├── Real
│   ├── Animal
│   │   ├── Species (antelope, bat, beaver,...)
│   ├── Human
│   ├── Landscape
├── Fooocus
│   ├── Animal
│   │   ├── Species (antelope, bat, beaver,...)
│   ├── Human
│   ├── Landscape
├── Flux_Canny
│   ├── Animal
│   │   ├── Species (antelope, bat, beaver,...)
│   ├── Human
│   ├── Landscape
├── RealVis4
│   ├── Animal
│   │   ├── Species (antelope, bat, beaver,...)
│   ├── Human
│   ├── Landscape
├── PhotoMaker_RealVis3.0
│   ├── Animal
│   │   ├── Species (antelope, bat, beaver,...)
│   ├── Human
│   ├── Landscape
├── DiffGAN (Human)
│   ├── Human
├── StyleGAN (Animal, Human)
│   ├── Animal
│   ├── Human
├── VAR (Animal, Landscape)
│   ├── Animal
│   │   ├── Species (antelope, bat, beaver,...)
│   ├── Landscape
├── PAR (Landscape)
│   ├── Landscape
```

## Tutorial
To train a detector with PhotoMaker, we should create a folder named imagenet_ai, as follows.
```
├── PhotoMaker
│   ├── train
│   │   ├── Animal
│   │   │   ├── 0_real
│   │   │   ├── 1_fake
│   │   ├── Human
│   │   │   ├── 0_real
│   │   │   ├── 1_fake
│   │   ├── Landscape
│   │   │   ├── 0_real
│   │   │   ├── 1_fake
│   ├── test
│   │   ├── ...
│   ├── val
│   │   ├── ...
```
The images from training generator should be put into the corresponding folder in 1_fake. WHile the images from real should be put into the corresponding folder in 0_fake. There are also the label of those images when training model.


## Detection Methods

We use the codes of detection methods provided in the corresponding paper. 
The codes are stored in detection_codes/ folder.

- [CNNSpot](https://github.com/PeterWang512/CNNDetection)
- [DIMD](https://github.com/grip-unina/DMimageDetection)
- [UnivFD](https://github.com/WisconsinAIVision/UniversalFakeDetect)
- [RINE](https://github.com/mever-team/rine)
- [Proxy](https://github.com/OlalaKuBin-QN/RealAI)
- [DIRE](https://github.com/zhendongwang6/dire)
- [PatchCraft](https://github.com/cvlcgabriel/PatchCraft)

## Real Images

We gather real images from those useful link.

- [Animal - Animals with
Attributes 2 (AwA2)](https://cvml.ista.ac.at/AwA2/)
- [Human - Easyportrait](https://github.com/hukenovs/easyportrait)
- [Landscape - LHQ1024](https://www.kaggle.com/datasets/dimensi0n/lhq-1024)

## Generators

We use the codes of generative models provided in the corresponding paper. 

- [Fooocus](https://github.com/lllyasviel/Fooocus)
- [Flux_Canny](https://huggingface.co/black-forest-labs/FLUX.1-Canny-dev)
- [RealVis4](https://huggingface.co/SG161222/RealVisXL_V4.0)
- [PhotoMaker_RealVis3.0](https://github.com/TencentARC/PhotoMaker)
- [Diffusion-GAN](https://github.com/Zhendong-Wang/Diffusion-GAN)
- [StyleGAN3](https://github.com/nvlabs/stylegan3)
- [Visual autoregressive modeling (VAR)](https://github.com/FoundationVision/VAR)
- [Parallelized autoregressive vi-
sual generation (PAR)](https://github.com/YuqingWang1029/PAR)


## Benchmark
- Table 3: Results of different pretrained methods and evaluated on different testing subsets. There are accuracy and AUC/AUROC


### Real Images

| Source | Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Real | Animal | 74.82 | 99.88 | 99.16 | 92.12 | 69.18 | 78.86 | 84.38 |
| Real | Human | 97.16 | 99.88 | 98.40 | 60.16 | 49.98 | 91.70 | 82.58 |
| Real | Landscape | 98.12 | 98.04 | 98.26 | 98.50 | 79.90 | 80.90 | 99.44 |
| **Real Total** | | **90.03** | **99.27** | **98.61** | **83.59** | **66.35** | **83.32** | **88.80** |

---

### Diffusion Models (DM)

#### Fooocus

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Animal | 6.28 | 0.16 | 0.02 | 37.86 | 8.84 | 6.08 | 37.44 |
| Human | 1.02 | 0.90 | 0.06 | 9.04 | 6.10 | 7.50 | 18.22 |
| Landscape | 7.96 | 1.00 | 0.02 | 3.20 | 15.54 | 26.96 | 53.42 |
| **Average Accuracy - AUC/AUROC** | **5.08-45.99** | **0.69-64.65** | **0.03-25.54** | **16.70-47.36** | **10.16-25.48** | **13.51-46.95** | **36.36-78.67** |

#### RealVis 4.0

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Animal | 0.64 | 99.82 | 0.36 | 69.68 | 9.20 | 12.52 | 85.24 |
| Human | 0.10 | 99.60 | 0.88 | 20.06 | 2.04 | 6.22 | 80.86 |
| Landscape | 4.46 | 97.86 | 0.72 | 44.84 | 40.36 | 20.48 | 96.74 |
| **Average Accuracy - AUC/AUROC** | **1.73-33.32** | **99.09-99.94** | **0.65-43.03** | **44.86-72.31** | **17.20-30.10** | **13.07-51.09** | **87.61-94.90** |

#### FLUX Canny

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Animal | 0.46 | 5.42 | 0.48 | 83.04 | 32.60 | 2.00 | 80.32 |
| Human | 0.54 | 9.84 | 0.34 | 54.52 | 30.72 | 0.14 | 65.32 |
| Landscape | 2.40 | 21.22 | 0.72 | 69.36 | 40.06 | 3.86 | 90.48 |
| **Average Accuracy - AUC/AUROC** | **1.13-31.88** | **12.16-93.69** | **0.51-44.53** | **68.97-85.78** | **34.46-47.51** | **2.00-23.90** | **78.71-92.94** |

#### PhotoMaker

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Animal | 0.28 | 77.20 | 0.70 | 42.50 | 19.46 | 8.06 | 79.10 |
| Human | 0.02 | 46.10 | 1.02 | 11.12 | 8.32 | 2.62 | 83.04 |
| Landscape | 0.40 | 54.86 | 3.82 | 21.48 | 23.28 | 12.86 | 95.78 |
| **Average Accuracy - AUC/AUROC** | **0.23-35.23** | **59.39-98.37** | **1.85-51.54** | **25.03-62.50** | **17.02-31.04** | **7.85-36.12** | **85.97-94.51** |

| DM Overall | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|------------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| **DM - AUC/AUROC** | **2.05-36.60** | **42.83-89.16** | **0.76-41.16** | **38.89-66.99** | **19.71-33.53** | **9.11-39.51** | **72.16-90.25** |

---

### GAN Models

#### Diffusion-GAN

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Human | 65.40 | 0.00 | 33.14 | 99.48 | 87.36 | 13.94 | 99.88 |
| **Average Accuracy - AUC/AUROC** | **65.40-36.60** | **0.00-53.66** | **33.14-94.20** | **99.48-99.72** | **87.36-79.00** | **13.94-59.40** | **99.88-99.73** |

#### StyleGAN3

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Animal | 29.54 | 0.02 | 9.62 | 76.10 | 45.70 | 11.78 | 99.84 |
| Human | 59.46 | 0.00 | 24.36 | 99.98 | 41.14 | 21.14 | 99.78 |
| **Average Accuracy - AUC/AUROC** | **44.50-76.28** | **0.01-52.09** | **16.99-88.12** | **88.04-90.76** | **43.42-54.61** | **16.46-56.64** | **99.81-99.43** |

| GAN Overall | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|------------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| **GAN - AUC/AUROC** | **54.95-82.38** | **0.01-53.70** | **25.07-90.52** | **93.76-95.00** | **65.39-69.07** | **15.20-56.43** | **99.85-99.71** |

---

### Autoregressive Models (AR)

#### VAR

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Animal | 17.10 | 75.18 | 36.22 | 87.80 | 70.20 | 15.48 | 97.38 |
| Landscape | 19.96 | 81.54 | 54.40 | 93.90 | 78.14 | 14.56 | 98.40 |
| **Average Accuracy - AUC/AUROC** | **18.53-65.16** | **78.36-98.98** | **45.31-92.43** | **90.85-98.40** | **74.17-81.11** | **15.02-44.05** | **97.89-98.77** |

#### PAR

| Category | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| Landscape | 29.22 | 45.12 | 52.18 | 56.06 | 59.08 | 15.06 | 98.32 |
| **Average Accuracy - AUC/AUROC** | **29.22-82.48** | **45.12-95.25** | **52.18-92.77** | **56.06-93.97** | **59.08-77.81** | **15.06-44.97** | **98.32-99.90** |

| AR Overall | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|------------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| **AR - AUC/AUROC** | **23.88-71.33** | **61.74-98.73** | **48.75-91.94** | **73.46-89.86** | **66.63-74.29** | **14.04-44.37** | **98.11-97.42** |

---

### Fake Images

| Metric | CNNSpot | DIMD | UnivFD | RINE | Proxy | DIRE | PatchCraft |
|----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| **Fake in Total** | **20.73** | **36.85** | **18.83** | **61.25** | **42.86** | **12.11** | **85.57** |
| **Overall Mean - AUC/AUROC** | **55.38-50.02** | **68.06-84.85** | **58.72-41.66** | **72.42-75.47** | **54.61-46.25** | **47.97-43.14** | **87.18-93.02** |

