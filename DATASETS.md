# Datasets — download links and required Google Drive layout

All datasets are public. Download each one, then upload it to your Google Drive using the
exact folder names shown below so the notebooks find them without editing paths.

## Coffee leaf datasets (5 sources)

| # | Dataset | Canonical (citable) source | Kaggle mirror used in the code |
|---|---------|----------------------------|--------------------------------|
| DS1 | **BRACOL** — Brazilian Arabica coffee leaves | https://data.mendeley.com/datasets/yy2k5y8mxg/1 (DOI 10.17632/yy2k5y8mxg.1) | https://www.kaggle.com/datasets/mohammedzwaughfa/coffee-leaf-disease-dataset |
| DS2 | **Coffee Leaves Disease** | (Kaggle-hosted) | https://www.kaggle.com/datasets/miladatulmuharromah/coffee-leaves-disease |
| DS3 | **Coffee Dataset (Mendeley mirror)** | (Kaggle-hosted mirror) | https://www.kaggle.com/datasets/trongtri04042004/coffee-dataset-mendeley |
| DS4 | **RoCoLe** — robusta coffee leaves, Ecuador | https://data.mendeley.com/datasets/c5yvn32dzg/2 (DOI 10.17632/c5yvn32dzg.2) | https://www.kaggle.com/datasets/nirmalsankalana/rocole-a-robusta-coffee-leaf-images-dataset |
| DS5 | **JMuBEN / JMuBEN2** — Arabica coffee leaves, Kenya | https://data.mendeley.com/datasets/t2r6rszp5c/1 and https://data.mendeley.com/datasets/tgv3zb82nd/1 (DOI 10.1016/j.dib.2021.107142) | https://www.kaggle.com/datasets/noamaanabdulazeem/jmuben-coffee-dataset |

## Cocoa pod dataset (1 source)

| Dataset | Link |
|---------|------|
| **Cocoa Diseases (preprocessed for YOLO)** — 5 classes, bounding-box labels | https://www.kaggle.com/datasets/bryandarquea/cocoa-diseases |

Related citable source for the underlying imagery/classes: *Dataset of Peruvian Cocoa Fruits
for Automatic Disease Detection*, IEEE DataPort — https://ieee-dataport.org/documents/dataset-peruvian-cocoa-fruits-automatic-disease-detection

## Required Google Drive folder structure

After downloading, arrange the files in your Drive exactly like this
(these names match the `DRIVE_ROOT` / `COCOA_ROOT` variables in the notebooks):

```
MyDrive/
├── coffee_datasets/
│   ├── coffee-leaf-disease-dataset/
│   │   └── dataset/
│   │       ├── Train/            # class sub-folders (Healthy, Miner, Phoma, Rust)
│   │       └── test/
│   ├── coffee-leaves-disease/
│   │   └── Coffee Leave Disease/ # class sub-folders
│   ├── coffee-dataset-mendeley/
│   │   └── coffee dataset/       # class sub-folders (Health leaves, leaf rust, phoma, ...)
│   ├── rocole-a-robusta-coffee-leaf-images-dataset/   # class sub-folders
│   └── jmuben-coffee-dataset/
│       └── JMuBEN/               # class sub-folders (Healthy, Miner, Phoma, Rust, ...)
│
├── cocoa_dataset/
│   └── cocoa_diseases/
│       ├── images/
│       ├── labels/               # YOLO .txt labels
│       └── notes.json
│
├── coffee_outputs/               # created automatically by the coffee notebooks
└── cocoa_outputs/                # created automatically by the cocoa notebook
```

## Notes on class mapping
The notebooks map each source's native class names onto the four shared coffee classes
(Healthy, Leaf Miner, Phoma, Rust) via the `*_MAP` dictionaries in the configuration cell;
classes present in only one source (e.g., Cercospora) are dropped for consistency. If a
downloaded folder uses slightly different class-folder names, update the corresponding
`*_MAP` dictionary — no other change is needed.

## Workflow on Google Colab
1. Download each dataset from the links above.
2. Upload them to Google Drive following the structure above.
3. Open a notebook in Colab, run the first cell to mount Drive, then run all cells.
   The coffee notebook reproduces Tables 1–6 and the classification figures; the cocoa
   notebook reproduces Table 7 and the detection figures.
