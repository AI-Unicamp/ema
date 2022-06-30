<!-- markdownlint-disable MD033 -->
<h1 align="center">
  <br>
     <img src="logo.png" alt="EMA logo" width="120" height="178">
  <br>
  EMA Project
  <br>
</h1>

<h4 align="center">A automatic metadata extractan project.</h4>
<p align="center">
  <a href="#about">About</a> •
  <a href="#scraper">Scraper</a> •
  <a href="#notebooks">Notebooks</a> •
  <a href="#processed-dataset">Processed dataset</a> •
  <a href="#credits">Credits</a> •
  <a href="#license">License</a>
</p>

## Scraper

The [scraper](./scraper/) directory contains the script needed to download, treat and create the EMA
database by thesaurus and labels. To execute, please follow the readme inside
the source folder.

## Notebooks

The [notebooks](./notebooks/) directory contains the resnet50 execution script and the exploratory part before the model
database achievement.

## Processed dataset
If you are interested in the dataset generate by default from the scraper script you can use the one applied to the iPres Conference. Access 
![here](https://drive.google.com/file/d/1FGllyNtNe57ALeJ9edeJv9-te1nbwURD/view). 

The dataset have the following structure:
```bash
dataset
├── bed
├── bottle
├── candlestick
├── chair
├── chandelier
├── chest
├── chest of drawers
├── cup
├── cup of tea
├── curtain
├── cutlery
├── dish
├── fork
├── glass
├── jug
├── kerosene lamp
├── lamp
├── lantern
├── luminaire
├── mirror
├── oratory
├── pan
├── platter
├── saucer
├── sconce
├── sideboard
├── spoon
├── table
├── table knife
├── vase
└── wardrobe
```
## Credits
Thanks to Amanda Oliveira, from IBRAM for the valuable information she provided regarding her experience in Brazilian museums. We also thank the Tainacan community for their support.
