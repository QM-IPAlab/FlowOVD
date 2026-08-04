# FlowOVD
Coming soon ;)

## :checkered_flag: Getting Started

### 1. Data Preparation

#### COCO
* Download [COCO](https://cocodataset.org/#download) from the official website, and put them on datas/coco folder.
  ```bash
  cd $root_dir
  mkdir -p datas/coco
  wget http://images.cocodataset.org/zips/train2017.zip -O datas/coco/train2017.zip
  wget http://images.cocodataset.org/zips/val2017.zip -O datas/coco/val2017.zip
  wget http://images.cocodataset.org/annotations/annotations_trainval2017.zip -O datas/coco/annotations_trainval2017.zip
  ```
* Extract the ziped files, and remove them:
  ```bash
  cd $root_dir
  unzip datas/coco/train2017.zip -d datas/coco
  unzip datas/coco/val2017.zip -d datas/coco
  unzip datas/coco/annotations_trainval2017.zip -d datas/coco
  rm datas/coco/train2017.zip datas/coco/val2017.zip datas/coco/annotations_trainval2017.zip
  ```

#### COCO-ReM
* COCO-ReM is hosted on Huggingface Datasets at [@kdexd/coco-rem]([https://cocodataset.org/#download](https://huggingface.co/datasets/kdexd/coco-rem)). Download the annotation files:
  ```bash
  cd $root_dir
  mkdir -p datas/coco-rem
  cd datas/coco-rem
  for name in trainrem valrem; do
    wget https://huggingface.co/datasets/kdexd/coco-rem/resolve/main/instances_$name.json.zip
    unzip instances_$name.json.zip
  done
  ```

#### LVIS
* Download LVIS annotation files:
  ```bash
  cd $root_dir
  mkdir -p datas/lvis
  wget https://huggingface.co/hao9610/OV-DINO/resolve/main/lvis_v1_minival_inserted_image_name.json -O datas/lvis/annotations/lvis_v1_minival_inserted_image_name.json
  wget https://huggingface.co/hao9610/OV-DINO/resolve/main/lvis_v1_val_inserted_image_name.json -O datas/lvis/annotations/lvis_v1_val_inserted_image_name.json
  ```
* Soft-link COCO to LVIS:
  ```bash
  cd $root_dir
  ln -s $(realpath datas/coco/train2017) datas/lvis
  ln -s $(realpath datas/coco/val2017) datas/lvis
  ```

#### Objects365
* Refer to the [OpenDataLab](https://opendatalab.com/OpenDataLab/Objects365_v1/cli/main) for Objects365V1 download, which has provided detailed download instruction.
  ```bash
  cd $root_dir
  mkdir -p datas/o365/annotations
  # Suppose you download the Objects365 raw file and put them on datas/o365/raw, extract the tared files and reorder them.
  cd datas/o365/raw
  tar -xvf Objects365_v1.tar.gz
  cd 2019-08-02
  for file in *.zip; do unzip -o "$file"; done
  mv *.json $root_dir/datas/o365/annotations
  mv train val test $root_dir/datas/o365
