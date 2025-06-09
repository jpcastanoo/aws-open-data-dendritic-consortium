# Dendritic Consortium Multimodal Dataset  
### Baz1a Neurons in Mouse Primary Visual Cortex (V1) and Hydra Vulgaris Endoderm Neurons

![Header](img/header.jpg)

## Summary
This dataset is generated through a collaboration of six leading neuroscience laboratories, collectively known as the Dendritic Consortium. It aims to redefine the traditional neuron model by focusing on dendrites as active computational units rather than passive inputs.

The dataset integrates multimodal data from Baz1a pyramidal neurons in the mouse primary visual cortex (V1) and the endoderm neurons of Hydra vulgaris. It includes high-resolution modalities such as in vivo voltage imaging, dendritic patch-clamp recordings, synaptic mapping, proteomics, volumetric EM-based maps, and computational neuronal models.

All experimental and computational data are made publicly available to accelerate neuroscience research and promote community collaboration.

## About
The Dendritic Consortium dataset challenges the traditional soma-centric view of neurons by focusing on the active computational role of dendrites. This paradigm shift is supported by combining data across molecular, structural, functional, and computational approaches.

Data is collected using state-of-the-art neuroscience methods across six leading research laboratories: Michael Lin's lab at Stanford University, Rafael Yuste's lab at Columbia University, Jayeeta Basu's lab at New York University, Elly Nedivi's lab at MIT, Jeff Lichtman's lab at Harvard University, and Idan Segev's lab at the Hebrew University of Jerusalem.

---

### Data Overview
- **Modalities**: Voltage imaging, electrophysiology data, synaptic mapping, proteomics, volumetric electron microscopy-based maps, computational modeling.
- **Species**: Mouse (Baz1a pyramidal neurons in V1), Hydra vulgaris (endoderm neurons).
- **Size**: Approx. 50–100 TB, growing at ~30 TB/year.
- **File formats**: TIFF, HDF5, GBK, ABF, PNG, PY, MAT, CSV, JSON, HOC, PKL, ASC/SWC.

### Update Cadence
The dataset is continuously expanding as participating laboratories within the consortium generate new experimental and computational data on a regular basis. 

### Data Available and File Formats
The dataset contains multimodal files capturing:

| Attribute               | Description                                                              |
|-------------------------|--------------------------------------------------------------------------|
| Voltage imaging files   | High temporal resolution optical voltage recordings in TIFF format.       |
| Calcium imaging files   | Optical recordings capturing calcium dynamics in TIFF or PNG format.      |
| Electrophysiology data  | Patch-clamp recordings in ABF, MAT, and CSV formats.                      |
| Synaptic mapping        | Data related to synaptic connections and interactions in CSV format.      |
| Proteomics              | Protein expression and synaptic marker data in CSV format.                |
| EM Volumes              | 3D volumetric electron microscopy maps in TIFF/PNG.                       |
| Computational models    | Neuronal morphologies and simulations in SWC, HOC, PY, PKL formats.       |
| Metadata                | Stored in a database accessible via a GUI. Access details will be announced. |

### Dataset Metadata
The dataset metadata is organized into several relational tables, each describing different aspects of the data stored in a public AWS S3 bucket. These tables provide context regarding data provenance, experimental conditions, parameters, and other details.

Below is a summary of the metadata tables included:

| Table Name             | Description                                                                                 | ID Prefix |
|------------------------|---------------------------------------------------------------------------------------------|-----------|
| [**analysis**](json-schemas/analysis.json)           | Files generated from computational/statistical analysis (graphs, reports, metrics).        | A         |
| [**behavior**](json-schemas/behavior.json)           | Quantitative/qualitative behavioral data recorded during experiments.                      | B         |
| [**cell_detection_dataset**](json-schemas/cell_detection_dataset.json) | Datasets of detected cell locations/types from segmentation tools.                         | CD        |
| [**ephys**](json-schemas/ephys.json)              | Electrophysiology recordings, e.g., dendritic patch-clamp data.                            | E         |
| [**image**](json-schemas/image.json)              | Imaging files capturing calcium, voltage, or fluorescence signals.                         | IMG       |
| [**micro_ct_dataset**](json-schemas/micro_ct_dataset.json)   | High-resolution micro-CT volumetric anatomical images.                                    | MD        |
| [**model**](json-schemas/model.json)              | Computational neuronal models simulating biophysical and morphological properties.         | MOD       |
| [**mouse**](json-schemas/mouse.json)              | Mouse specimen metadata including strain, genotype, birth date, etc.                       | M / L     |
| [**plasmid**](json-schemas/plasmid.json)            | Plasmids used for genetic constructs (e.g. GEVIs, opsins).                                | P         |
| [**sem_dataset**](json-schemas/sem_dataset.json)        | Scanning electron microscopy datasets with ultrastructural details.                       | SD        |
| [**session**](json-schemas/session.json)            | Data acquisition events metadata (experimenter, date, anesthesia, etc.).                   | S         |
| [**virus**](json-schemas/virus.json)              | Information on AAV vectors used for genetic delivery.                                     | V         |

Detailed descriptions of each table's attributes (columns), including types and descriptions, are available in the [metadata.md](metadata.md) file. The metadata is organized by table name, with JSON schema files available in the [json-schemas/](json-schemas) directory.

---

## Access and Structure
The dataset will be hosted on AWS S3 with a structured directory layout to facilitate scalable cloud access:
```
s3://dendritic-consortium-open-data/
├── lab-name/             ← Root folder for each participating lab
  ├── YYYYMMDD/           ← Date of the experimental session
    ├── object-type/      ← Data modality or type (e.g., image, ephys, sem_dataset)
      ├── version/        ← Data version (raw, processed, roi, script)
        ├── files/        ← Actual data files
```
Data access will be open with no sign-in required for downloads. Detailed access instructions and AWS CLI examples will be provided once the dataset is publicly available.

## Tutorials
Tutorials to guide users through accessing and analyzing the dataset on AWS cloud are planned for future release.

## License
This dataset is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

This dataset is a collaboration between Columbia University, Stanford University, New York University, Harvard University, MIT, and Hebrew University of Jerusalem.
