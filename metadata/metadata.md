# Metadata

This document provides detailed descriptions of each table's attributes (columns), including their **data types** and **descriptions**. It serves as a guide for understanding the structure and content of the metadata associated with the open dataset available on AWS.

## ID Naming Convention

Each record in this dataset is assigned a **unique identifier (ID)** that follows a specific naming convention to ensure consistency and traceability across different types of data. The ID is structured as follows:

    [Lab Initials]_[Object Prefix]_[Four-digit number with leading zeros]

For example: **`RY_IMG_0001`** would represent the first image file entered by the Yuste lab. The object prefix (e.g., `IMG`, `E`, `B`) corresponds to the type of object, which is defined in the respective table for each object type.

---

## Object Types per Lab

Each lab works with a distinct set of **data objects** based on their specific research focus. The following table outlines the available object types for each lab:

- **Michael Lin (ML)**: virus, plasmid, mouse, session, image, analysis.
- **Rafael Yuste (RY)**: virus, mouse, session, image, ephys, analysis.
- **Jayeeta Basu (JB)**: mouse, session, image, ephys, behavior, analysis.
- **Elly Nedivi (EN)**: plasmid, mouse, session, image, analysis.
- **Jeff Lichtman (JL)**: cell_detection_dataset, micro_ct_dataset, sem_dataset, analysis.
- **Idan Segev (IS)**: model, analysis.

Each object type has a corresponding **prefix** that must be used in the ID to distinguish different object categories. For example, the object type **image** has the prefix `IMG`, and **analysis** has the prefix `A`.

---

## Key Definitions

- **PK (Primary Key)**: A unique identifier for a record in a table.
- **FK (Foreign Key)**: A reference to a primary key (PK) in another table, establishing relationships between tables.

---

## Data Type Glossary

Here is a list of data types used across the metadata schema:

- **ID**: A unique identifier for each record.
- **str**: A text string.
- **int**: An integer number.
- **float**: A decimal number.
- **bool**: A boolean value.
- **date**: A date in the YYYYMMDD format.
- **time**: Time in 24-hour format (HH:MM).

---

## List of Objects

### `analysis` Table

Any file generated from computational or statistical analysis, including visualizations, metrics, graphs, or reports. Object-specific prefix for ids: **A**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `analysis_id (PK)`    | ID       | Unique analysis output identifier                                 |
| `source_type`         | str      | Type of source file (e.g., image, ephys, sem_dataset)             |
| `source_id (FK)`      | ID       | ID of the analyzed file                                           |
| `description`         | str      | Description of graph or report                                    |
| `file_path`           | str      | S3 path to analysis output file                                   |
| `notes`               | str      | Additional comments                                              |

---

### `behavior` Table

Quantitative and/or qualitative behavioral data (e.g., movement, task performance) obtained during experimental sessions. Object-specific prefix for IDs: **B**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `behavior_id (PK)`    | ID       | Unique behavior file identifier                                   |
| `session_id (FK)`     | ID       | Associated session                                               |
| `metric_type`         | str      | Behavioral metric type (e.g. locomotion, freezing)                |
| `task`                | str      | Task performed by subject                                        |
| `injection`           | str      | Drug injected (if any)                                            |
| `file_path_raw`       | str      | S3 path to raw file                                              |
| `file_path_processed` | str      | S3 path to processed file                                         |
| `file_path_script`    | str      | S3 path to script file                                           |
| `notes`               | str      | Additional comments                                              |

---

### `cell_detection_dataset` Table

Dataset containing detected cell locations and/or types, typically generated using segmentation tools. Object-specific prefix for IDs: **CD**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `cell_dataset_id (PK)`| ID       | Unique cell detection dataset identifier                          |
| `mouse_id (FK)`       | ID       | Associated mouse identifier                                       |
| `tool`                | str      | Software or algorithm used for cell detection                     |
| `start_date`          | date     | Start date for dataset acquisition                                |
| `end_date`            | date     | End date for dataset acquisition                                  |
| `file_path_local`     | str      | Local path to dataset file                                        |
| `file_path`           | str      | S3 path to dataset file                                           |
| `notes`               | str      | Additional comments                                              |

---

### `ephys` Table

Electrophysiological trace data (e.g., dendritic patch-clamp recordings). Object-specific prefix for IDs: **E**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `ephys_id (PK)`       | ID       | Unique electrophysiology file identifier                          |
| `session_id (FK)`     | ID       | Associated session                                               |
| `recording_type`      | str      | Type of recording (e.g. dendritic patch, ex vivo, in vivo)        |
| `processing_methods`  | str      | Processing methods applied                                        |
| `sampling_rate`       | float    | Sampling rate in Hertz (Hz)                                       |
| `file_path_raw`       | str      | S3 path to raw file                                              |
| `file_path_processed` | str      | S3 path to processed file                                         |
| `file_path_script`    | str      | S3 path to script file                                           |
| `notes`               | str      | Additional comments                                              |

---

### `image` Table

File or stack of images capturing intracellular calcium dynamics, membrane voltage, or fluorescence signal using indicators (e.g., GECIs, GEVIs). Object-specific prefix for IDs: **IMG**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `image_id (PK)`       | ID       | Unique file identifier                                            |
| `session_id (FK)`     | ID       | Associated session                                               |
| `image_type`          | str      | Type of image (e.g. voltage, calcium, fluorescence)               |
| `frame_rate`          | float    | Acquisition rate in Hertz (Hz)                                    |
| `x`                   | int      | Image width in pixels (horizontal dimension)                      |
| `y`                   | int      | Image height in pixels (vertical dimension)                       |
| `z`                   | int      | Number of images on stack (stack depth)                           |
| `pixel_size`          | float    | Size of each pixel in micrometers (µm/pixel)                      |
| `numerical_aperture`  | float    | Objective numerical aperture                                      |
| `objective_magn`      | str      | Objective magnification (e.g. 20x, 40x)                            |
| `exposure_time`       | float    | Exposure time per frame in milliseconds (ms)                      |
| `laser_power`         | float    | Laser power used in milliwatts (mW)                               |
| `laser_line`          | int      | Wavelength of laser used in nanometers (nm)                       |
| `processing_methods`  | str      | Methods used in image processing                                  |
| `roi_tool`            | str      | Software/tool used for ROI annotation (if any)                    |
| `file_path_raw`       | str      | S3 path to raw image file or stack                                |
| `file_path_processed` | str      | S3 path to processed image file or stack                          |
| `file_path_roi`       | str      | S3 path to ROI annotation file                                    |
| `file_path_script`    | str      | S3 path to processing script                                      |
| `notes`               | str      | Additional comments                                              |

---

### `micro_ct_dataset` Table

High-resolution volumetric image obtained via micro-CT for detailed anatomical analysis. Object-specific prefix for IDs: **MD**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `micro_ct_id (PK)`    | ID       | Unique micro-CT dataset identifier                                |
| `mouse_id (FK)`       | ID       | Associated mouse identifier                                       |
| `voxel_size`          | float    | Voxel resolution in micrometers (µm)                              |
| `contrast_agent`      | str      | Contrast agent used (if any)                                      |
| `start_date`          | date     | Start date for dataset acquisition                                |
| `end_date`            | date     | End date for dataset acquisition                                  |
| `file_path_local`     | str      | Local path to dataset file                                        |
| `file_path`           | str      | S3 path to dataset file                                           |
| `notes`               | str      | Additional comments                                              |

---

### `model` Table

Computational model designed to simulate neuronal biophysics, physiology, and morphology at synaptic resolution, integrating multimodal data (e.g., imaging, electrophysiology, behavior). Object-specific prefix for IDs: **MOD**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `model_id (PK)`       | ID       | Unique model identifier                                           |
| `model_type`          | str      | Type of model (e.g. biophysical, deep neural network)             |
| `model_version`       | str      | Version identifier for model iteration                            |
| `file_path_model`     | str      | S3 path to compiled/saved model                                   |
| `file_path_script`    | str      | S3 path to script used for model construction                     |
| `description`         | str      | Description of the model                                          |
| `notes`               | str      | Additional comments                                              |

---

### `mouse` Table

Laboratory mouse serving as the source of experimental data. Object-specific prefix for IDs: **L** for litter and **M** for mouse

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `litter_id`           | ID       | Unique litter identifier                                          |
| `mouse_id (PK)`       | ID       | Unique mouse identifier                                           |
| `strain`              | str      | Mouse strain. Use semicolons to separate double transgenic lines (e.g. Camk2a-Cre;Ai162) |
| `genotype`            | str      | Allelic state of each transgene. Use semicolons to separate loci (e.g. “+/-;+/-” for double transgenic) |
| `cre_line`            | str      | Cre driver line, if applicable (e.g. Camk2a-Cre)                  |
| `sex`                 | str      | Biological sex (M or F)                                           |
| `birth_date`          | date     | Date of birth (e.g 20250101)                                      |
| `weight`              | float    | Body weight in grams                                              |
| `plasmid_id (FK)`     | ID       | Plasmid used (if any)                                             |
| `virus_id (FK)`       | ID       | AAV used (if any)                                                 |
| `notes`               | str      | Additional comments                                              |

---

### `plasmid` Table

Circular DNA molecule used to deliver and express specific genetic material (e.g. GEVIs, opsins, fluorescent proteins) in targeted cells. Object-specific prefix for IDs: **P**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `plasmid_id (PK)`     | ID       | Unique plasmid identifier                                         |
| `plasmid_name`        | str      | Full name of the plasmid                                          |
| `gene`                | str      | Gene encoded by the plasmid (e.g. GCaMP6, tdTomato)              |
| `indicator`           | str      | Type of reporter protein (e.g. voltage/calcium indicator, optogenetic actuator) |
| `wavelength`          | int      | Emission peak in nanometers                                       |
| `backbone`            | str      | Vector backbone used (e.g. pAAV)                                  |
| `promoter`            | str      | Promoter driving expression (e.g. syn, Camk2a, CAG)              |
| `tuning`              | str      | Polarity of response, if applicable (e.g. positive, negative)     |
| `notes`               | str      | Additional comments                                              |

---

### `sem_dataset` Table

Ultrastructural dataset generated by scanning electron microscopy (SEM), providing high-resolution cellular detail. Object-specific prefix for IDs: **SD**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `sem_dataset_id (PK)` | ID       | Unique SEM dataset identifier                                     |
| `mouse_id (FK)`       | ID       | Associated mouse identifier                                       |
| `section`             | str      | Related brain section                                             |
| `resolution`          | float    | Pixel resolution in nanometers (nm/pixel)                         |
| `start_date`          | date     | Start date for dataset acquisition                                |
| `end_date`            | date     | End date for dataset acquisition                                  |
| `file_path_local`     | str      | Local path to dataset file                                        |
| `file_path_raw`       | str      | S3 path to raw dataset file                                       |
| `file_path_processed` | str      | S3 path to processed dataset (alignment and stitching)            |
| `file_path_viewer`    | str      | S3 path to dataset in a compatible format for viewer tool         |
| `file_path_script`    | str      | S3 path to script used for processing                             |
| `notes`               | str      | Additional comments                                              |

---

### `session` Table

Data acquisition event in which imaging (e.g., two-photon, confocal, or SEM) or electrophysiological data is collected on one mouse. Object-specific prefix for IDs: **S**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `session_id (PK)`     | ID       | Unique session identifier                                         |
| `mouse_id (FK)`       | ID       | Associated mouse identifier                                       |
| `experimenter`        | str      | Experimenter’s first and last name                                |
| `session_date`        | date     | Date of session (e.g 20250101)                                    |
| `start_time`          | time     | Start time of session                                             |
| `end_time`            | time     | End time of session                                               |
| `anesthesia`          | str      | Name of analgesic (if any)                                        |
| `notes`               | str      | Additional comments                                              |

---

### `virus` Table

Recombinant adeno-associated virus (AAV) used to deliver genetic material to cells in vivo. Object-specific prefix for IDs: **V**

| **Attribute**         | **Type** | **Description**                                                   |
|-----------------------|----------|-------------------------------------------------------------------|
| `virus_id (PK)`       | ID       | Unique AAV identifier                                             |
| `virus_name`          | str      | Full name of the AAV                                              |
| `plasmid_id (FK)`     | ID       | Linked plasmid ID                                                |
| `serotype`            | str      | AAV serotype (e.g. AAV1, AAV9)                                    |
| `floxed`              | bool     | TRUE if expression is Cre-dependent, FALSE if not                |
| `titer`               | str      | Viral concentration in genome copies per mL (GC/mL)              |
| `notes`               | str      | Additional comments                                              |
