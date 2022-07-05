# Extração Automática de Metadados (EMA)

## Standard EMA database creation

The standard database creation has fixed parameters founded with a data
exploration aiming to tackle EMA project.

To use de standard database go straight to the execution session.

## Custom database creation

To create a custom database it is necessary to change and update the following
variables at the constants.py file:

* TESAURO: the desired thesaurus classification
* MUSEUM_DICT: update the museum's pages
* Add the museum acronym and field.
* TL_JOINED: add the desired target labels in portuguese and english.
* TL_BW: Update the target label bad words dict.

After changing and update those variables it is possible to create the database.

## Execution

### Using docker

With docker, it is possible straight forward with one command:

```bash
docker-compose up
```

**NOTE:** The full completion may take while due to the images database size.

**Output:** The modeldb is generated at ```data``` directory.

### From script &mdash; One command

It is possible to download the whole database, text and images, with one python
execution command:

```bash
python database create_model_db
```

The output is a ```data``` directory in containing all raw, interim
and processed data. The model dataset is inside the processed one.

### From script &mdash; Step by step

#### Download the whole text database

Download text database in JSON format from each Museum. Every file corresponds
to one item.  

The JSON file's name stored are structured as follows:

```bash
{museum_acr}_{item_id}.json
```

Where:

* `museum_acr`: museum acronym
* `item_id`: item identification

#### Usage

```bash
python database.py fetch_jsons
```
  
**Output:** ```data/raw/jsons```

### Download the whole images database

Download images database from each Museum. The data is scraped from each Museum
website, with all its related items. The images URLs are gathered from the JSON
files at *raw JSON database*. An image file name is structured as follows:

```bash
{museum_acr}_{item_id}_{item_number}.{format}
```

Where:

* `museum_acr`: museum acronym
* `item_id`: item identification
* `item_number`: number of the image in the sequence gathered from the website.
Be aware that this ID is only available to distinguish images from the same
item at the downloaded database.
* `format`: image format at the data base

#### Usage

```bash
python database.py fetch_images
```

**Output:** ```data/raw/images```

-----------

**NOTE:** The images will be downloaded only if the JSON files where
downloaded, so if the JSON folder is empty, the images module will trigger
that module first and, the starts after finish.

-----------

### Classify JSON by Thesaurus and Refined Labels

This step will get all JSON data classified by its thesaurus type and
save in the interim folder and after that will save all JSON that matches
the refined labels passed as list into to the processed folder. This step is
required to gain the thesaurus images for interim and processed image files.

Execution script -- Text:

1. By thesaurus

```bash
python database.py classify_jsons_by_thesaurus
```

Output: ```data/interim/jsons```
**NOTE:** The default Thesaurus is Interior, code 05. 

2. By labels

```bash
python database.py classify_jsons_by_labels
```

**Output:** ```data/processed/jsons```

### Classify images by Thesaurus or list of labels

Takes the classified JSON and its ID to get the images in the raw database
and copy them to the interim database. The classification by labels is made by
passing a list of labels to the same script and after that is saved in to the
processed images folder. Will only be trigged if the JSON exists.

Execution script -- Images:

1. By Thesaurus

```bash
python database.py classify_imgs_by_thesaurus
```

**Output:** ```data/interim/images```
**NOTE:** The default Thesaurus is Interior, code 05. 

2. By labels

```bash
python database.py classify_imgs_by_labels
```

**Output:** ```data/processed/images```

### Build the refined dataset

The refined dataset, called modeldb, is structured by labels and have all
duplicated images removed. This dataset is ready to be used in multi-label
classification models.

```bash
python database create_model_db
```

The output is a ```data``` directory in containing all raw, interim
and processed data. The model dataset is inside the processed one.

### Project Structure

```bash
├── data
│   ├── interim
│   │   ├── images
│   │   └── jsons
│   ├── processed
│   │   ├── images
│   │   └── jsons
│   └── raw
│       ├── images
│       └── jsons
├── helpers
│   ├── auxiliar.py
│   └── constants.py
├── modules
│   ├── classify_images.py
│   ├── classify_jsons.py
│   ├── fetch_images.py
│   └── fetch_jsons.py
└── workspace
    ├── bad_requests.txt
```
