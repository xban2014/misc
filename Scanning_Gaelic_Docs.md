# Scanning Gaelic Documents

## Prerequisite Installs

These were done on a linux machine running Ubuntu:

- Poppler utilities for splitting PDF's into images: `sudo apt-get install poppler-utils`
- Install the `tesseract` OCR program from the ppa below:

```bash
sudo add-apt-repository ppa:alex-p/tesseract-ocr-devel
sudo apt update
apt list --upgradable
sudo apt update
sudo apt upgrade --yes

# Scottish Gaelic module:
sudo apt install tesseract-ocr-gla

# Irish module:
sudo apt install tesseract-ocr-gle 
```

## Scanning

1. Split the PDF into images, one image for each page, choose a 300dpi resolution:

```bash
mkdir sermons_binder_a1_pt_1_page_images
cd sermons_binder_1_pt_1_page_images

# input is the pdf file, each output image will be called sermons_binder_1_pt_1_page-NNN
pdftoppm -png -r 300 ../sermons_binder_1_pt_1.pdf sermons_binder_1_pt_1_page
```

2. For each of the images in the folder, do the OCR:

```bash
# create a folder to hold the converted text:
mkdir sermons_binder_1_pt_1_page_text 

# convert each file from the image folder into a text file in the text folder:
for pi in sermons_binder_1_pt_1_page_images/*.png; do echo $pi; b=`basename $pi .png`; echo $b; tesseract $pi sermons_binder_1_pt_1_page_text/$b -l gla+gle; done
```
